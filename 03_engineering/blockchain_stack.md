# Stack Blockchain

> Arquitectura detallada de blockchain para Meta Build City.
> Foco: smart contracts para construccion, tokenizacion, trazabilidad.
> Ultima actualizacion: Febrero 2026

---

## 1. Smart Contracts

### 1.1 Lenguaje y Frameworks

| Componente | Tecnologia | Version | Proposito |
|------------|-----------|---------|-----------|
| Lenguaje | Solidity | 0.8.20+ | Desarrollo de smart contracts |
| Framework principal | Hardhat | 2.x | Compilacion, testing, deployment, scripting |
| Framework secundario | Foundry (forge) | Latest | Fuzzing, gas profiling, testing avanzado |
| Librerias | OpenZeppelin Contracts | 5.x | Contratos base auditados |
| Typings | TypeChain | 8.x | TypeScript bindings para contratos |

### 1.2 Testing Strategy

**Niveles de testing**:

| Nivel | Herramienta | Cobertura | Descripcion |
|-------|------------|-----------|-------------|
| Unit Tests | Hardhat (Mocha/Chai) | Cada funcion publica/externa | Test individual de funciones |
| Integration Tests | Hardhat | Interaccion entre contratos | Test de flujos completos |
| Fuzz Testing | Foundry (forge test) | Edge cases, inputs aleatorios | Buscar vulnerabilidades con inputs random |
| Invariant Testing | Foundry | Propiedades que siempre deben cumplirse | Ej: "balance total == sum(balances individuales)" |
| Gas Profiling | Foundry (forge snapshot) | Todas las funciones | Medir y optimizar gas consumption |
| Fork Testing | Hardhat/Foundry | Interaccion con contratos existentes | Test contra estado real de mainnet |

**Coverage target**: >= 95% para contratos en produccion.

**Estructura de tests**:
```
test/
  unit/
    MilestonePayment.test.ts
    MaterialTraceability.test.ts
    QualityCertification.test.ts
  integration/
    PaymentFlow.test.ts
    SupplyChainFlow.test.ts
  fuzz/
    MilestonePayment.fuzz.t.sol
  invariant/
    MilestonePayment.invariant.t.sol
  gas/
    GasReport.test.ts
```

### 1.3 Auditing

**Herramientas automatizadas**:

| Herramienta | Tipo | Proposito |
|-------------|------|-----------|
| Slither (Trail of Bits) | Static analysis | Detectar vulnerabilidades comunes |
| Mythril (ConsenSys) | Symbolic execution | Analisis profundo de paths de ejecucion |
| Aderyn | Static analysis (Rust-based) | Deteccion rapida de issues |
| Solhint | Linter | Style guide y mejores practicas |
| Surya | Visualization | Grafos de herencia y llamadas |

**Manual Review Checklist**:
- [ ] Reentrancy: todas las funciones que transfieren ETH/tokens estan protegidas
- [ ] Access control: roles correctamente asignados y verificados
- [ ] Integer overflow: Solidity 0.8.x maneja automaticamente, pero verificar unchecked blocks
- [ ] Front-running: operaciones sensibles protegidas (commit-reveal si necesario)
- [ ] Gas limits: funciones no pueden consumir gas ilimitado (loops acotados)
- [ ] External calls: manejo correcto de return values y reverts
- [ ] Upgradability: storage layout correcto para proxies UUPS
- [ ] Events: todos los cambios de estado emiten events
- [ ] Input validation: require statements para todos los parametros
- [ ] Centralization risks: funciones admin documentadas y con timelock si necesario

**Proceso de auditoria**:
1. Self-audit con herramientas automatizadas (Slither, Mythril)
2. Peer review interno (minimo 2 revisores)
3. Auditoria externa para contratos de alto valor (Bug bounty o firma de auditoria)
4. Periodo de testing en testnet (minimo 2 semanas)
5. Deployment gradual (testnet -> staging -> mainnet con limits)

### 1.4 Design Patterns

**Patterns utilizados**:

| Pattern | Implementacion | Uso en MBC |
|---------|---------------|------------|
| UUPS Proxy | OpenZeppelin UUPSUpgradeable | Contratos que necesitan upgrades (MilestonePayment, Registry) |
| Access Control | OpenZeppelin AccessControl | Roles: ADMIN, OPERATOR, AUDITOR, CLIENT |
| Reentrancy Guard | OpenZeppelin ReentrancyGuard | Todas las funciones que transfieren valor |
| Pausable | OpenZeppelin Pausable | Emergency stop en todos los contratos |
| Pull Payment | OpenZeppelin PullPayment | Retiros de fondos (evitar push payments) |
| Multi-sig | Gnosis Safe | Aprobacion de milestones, admin operations |
| Timelock | OpenZeppelin TimelockController | Cambios administrativos con delay |
| Merkle Proof | Custom | Verificacion eficiente de listas de documentos |

---

## 2. Contract Templates para Construccion

### 2.1 MilestonePayment.sol

**Proposito**: Pagos escrow liberados al completar hitos del proyecto.

**Flujo**:
```
[Cliente deposita fondos]
    |
    v
[Contrato Escrow] <--- Fondos bloqueados
    |
    v
[Contratista completa milestone]
    |
    v
[Contratista sube evidencia (hash de fotos/docs en IPFS)]
    |
    v
[Aprobacion multi-sig]:
    - Firma 1: Representante del cliente
    - Firma 2: Supervisor de obra (ITO)
    - Regla: 2 de 2 (configurable a 2 de 3)
    |
    v
[Fondos liberados al contratista]
    |
    v
[Evento emitido: MilestoneCompleted(milestoneId, amount, timestamp)]
```

**Funciones principales**:
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

interface IMilestonePayment {
    struct Milestone {
        string description;
        uint256 amount;
        uint256 deadline;
        bytes32 evidenceHash;    // IPFS CID hash
        MilestoneStatus status;
        uint256 completedAt;
    }

    enum MilestoneStatus { Pending, Submitted, Approved, Paid, Disputed }

    function createProject(
        address contractor,
        string[] calldata descriptions,
        uint256[] calldata amounts,
        uint256[] calldata deadlines
    ) external payable returns (uint256 projectId);

    function submitEvidence(
        uint256 projectId,
        uint256 milestoneId,
        bytes32 evidenceHash
    ) external;

    function approveMilestone(
        uint256 projectId,
        uint256 milestoneId
    ) external;

    function claimPayment(
        uint256 projectId,
        uint256 milestoneId
    ) external;

    function disputeMilestone(
        uint256 projectId,
        uint256 milestoneId,
        string calldata reason
    ) external;

    event ProjectCreated(uint256 indexed projectId, address client, address contractor);
    event MilestoneSubmitted(uint256 indexed projectId, uint256 milestoneId, bytes32 evidenceHash);
    event MilestoneApproved(uint256 indexed projectId, uint256 milestoneId);
    event PaymentClaimed(uint256 indexed projectId, uint256 milestoneId, uint256 amount);
    event MilestoneDisputed(uint256 indexed projectId, uint256 milestoneId, string reason);
}
```

**Consideraciones**:
- Gas optimization: packed storage para Milestone struct
- Reentrancy protection en claimPayment
- Timelock de 48 horas entre aprobacion y claim (seguridad)
- Dispute resolution: arbitro designado puede resolver disputas
- Partial payments: soporte para pagos parciales en milestones grandes

### 2.2 MaterialTraceability.sol

**Proposito**: Trazabilidad de materiales desde proveedor hasta instalacion en obra.

**Basado en**: ERC-1155 (multi-token, cada tipo de material es un token ID)

**Flujo**:
```
[Proveedor registra lote de material]
    Token ID: tipo de material (acero, cemento, etc.)
    Metadata: proveedor, certificado de calidad, fecha, lote
    Cantidad: unidades del lote
    |
    v
[Transfer: Proveedor -> Transporte]
    Evento: MaterialShipped
    Metadata: guia de despacho, transportista
    |
    v
[Transfer: Transporte -> Obra (Bodega)]
    Evento: MaterialReceived
    Metadata: responsable de recepcion, fotos, estado
    |
    v
[Transfer: Bodega -> Ubicacion en Obra]
    Evento: MaterialInstalled
    Metadata: ubicacion BIM (nivel, zona, elemento), instalador
    |
    v
[Certificacion de calidad]
    Evento: QualityVerified
    Metadata: resultado de ensayo, certificador, fecha
```

**Metadata on IPFS** (por cada transfer event):
```json
{
  "materialType": "Acero A630-420H",
  "supplier": "Aceros del Pacifico",
  "batchNumber": "AP-2026-00123",
  "certificationUrl": "ipfs://Qm...",
  "photos": ["ipfs://Qm...", "ipfs://Qm..."],
  "specs": {
    "diameter_mm": 12,
    "length_m": 12,
    "fy_MPa": 420,
    "fu_MPa": 630
  },
  "timestamp": "2026-02-12T10:30:00Z",
  "geoLocation": {
    "lat": -33.4489,
    "lng": -70.6693
  }
}
```

### 2.3 QualityCertification.sol

**Proposito**: Registro inmutable de ensayos y certificaciones de calidad.

**Basado en**: Soulbound Tokens (SBT) - ERC-721 no transferible.

**Tipos de certificacion**:

| Tipo | Descripcion | Datos Registrados |
|------|-------------|-------------------|
| Probeta de hormigon | Ensayo de resistencia a compresion | f'c target, f'c real, edad, laboratorio |
| Soldadura | Ensayo no destructivo (END) | Tipo END, resultado, soldador, posicion |
| Compactacion de suelo | Densidad in-situ | Densidad seca, humedad, Proctor |
| Estanqueidad | Prueba de presion en tuberias | Presion, duracion, resultado |
| Resistencia al fuego | Certificacion de elementos | Clasificacion F, laboratorio |
| Aislacion termica | Certificacion de envolvente | R-value, certificador |

**Funcionalidad clave**:
- Token es non-transferable (soulbound): no se puede mover de un proyecto a otro
- Metadata inmutable: una vez emitido, no se puede modificar
- Verificacion publica: cualquiera puede verificar la autenticidad del certificado
- Batch minting: emitir multiples certificados en una transaccion
- Revocation: posibilidad de revocar (marcar como invalido) con razon documentada

### 2.4 ProjectRegistry.sol

**Proposito**: Registro central de proyectos con metadata y hashes de documentos clave.

**Datos on-chain**:
```solidity
struct Project {
    bytes32 projectId;           // Hash unico del proyecto
    address owner;               // Wallet del propietario/mandante
    string name;                 // Nombre del proyecto
    string location;             // Ubicacion (comuna, region)
    uint256 startDate;           // Fecha de inicio
    uint256 estimatedEndDate;    // Fecha estimada de termino
    ProjectStatus status;        // Planning, InProgress, Completed, Paused
    bytes32 bimModelHash;        // Hash del modelo BIM principal
    bytes32[] documentHashes;    // Hashes de documentos clave
    address[] stakeholders;      // Wallets de partes involucradas
}
```

**Integracion con otros contratos**:
- Link a MilestonePayment: proyecto tiene N milestone contracts
- Link a MaterialTraceability: materiales trackean project ID
- Link a QualityCertification: certificaciones referencian project ID

### 2.5 TokenizedProperty.sol

**Proposito**: Tokenizacion de propiedad inmobiliaria para inversion fraccionada.

**Basado en**: ERC-1155 (cada propiedad es un token ID, multiples fracciones por propiedad)

**Funcionalidad**:
```
[Desarrollador registra propiedad]
    Property ID: identificador unico
    Total fractions: 1000 (cada fraccion = 0.1% de la propiedad)
    Price per fraction: calculado del valor de tasacion
    |
    v
[Investors compran fracciones]
    KYC/AML verificado off-chain, whitelisted on-chain
    Pago en stablecoin (USDC) o fiat (via on-ramp)
    Tokens de fraccion emitidos al investor
    |
    v
[Distribucion de ingresos]
    Arriendos cobrados off-chain
    Distribuidos proporcionalmente a holders on-chain
    |
    v
[Secondary market]
    Holders pueden vender fracciones a otros investors whitelisted
    Precio de mercado determinado por oferta/demanda
    |
    v
[Exit / Venta de propiedad]
    Venta de propiedad completa
    Distribucion proporcional del precio de venta
    Burn de tokens
```

**Consideraciones regulatorias**:
- Clasificacion como valor (security token) bajo regulacion CMF Chile
- KYC/AML obligatorio para todos los participantes
- Whitelist on-chain: solo wallets verificadas pueden recibir tokens
- Compliance con Ley de Mercado de Valores
- Sandbox regulatorio de la CMF (si disponible)

---

## 3. Infraestructura

### 3.1 Networks

**Produccion**:

| Red | Chain ID | Uso | RPC |
|-----|----------|-----|-----|
| Polygon PoS | 137 | Contratos principales (bajo gas cost) | Alchemy |
| Ethereum Mainnet | 1 | Activos de alto valor, ancla de seguridad | Alchemy |
| Arbitrum One | 42161 | Alternativa para DeFi integrations | Alchemy |

**Testing**:

| Red | Chain ID | Uso | Faucet |
|-----|----------|-----|--------|
| Sepolia | 11155111 | Testing de contratos L1 | sepoliafaucet.com |
| Polygon Amoy | 80002 | Testing de contratos L2 | faucet.polygon.technology |
| Hardhat Network | 31337 | Testing local, fork testing | Built-in |
| Anvil (Foundry) | 31337 | Testing local rapido | Built-in |

### 3.2 RPC Providers

| Provider | Uso | Plan |
|----------|-----|------|
| Alchemy | RPC principal, Enhanced APIs, webhooks | Growth ($49/month) |
| Infura | RPC backup, IPFS gateway | Free tier |
| QuickNode | Alternativa si Alchemy tiene downtime | Free tier |

**Configuracion de fallback**:
```typescript
const providers = [
  new AlchemyProvider(chainId, ALCHEMY_API_KEY),
  new InfuraProvider(chainId, INFURA_API_KEY),
  new QuickNodeProvider(chainId, QUICKNODE_URL),
];
const fallbackProvider = new FallbackProvider(providers);
```

### 3.3 Storage Descentralizado

**IPFS (via Pinata)**:
- Uso: documentos de proyecto, fotos de evidencia, metadata de NFTs
- Plan: Picnic ($0) para desarrollo, Submarine ($20/month) para produccion
- Pinning: automatico via API al subir contenido
- Gateway: gateway dedicado de Pinata para acceso rapido

**Arweave**:
- Uso: documentos que deben ser permanentes (certificaciones, contratos firmados)
- Costo: pago unico por almacenamiento permanente (~$5/GB)
- Integracion: Bundlr/Irys para batched uploads eficientes

**Estructura de almacenamiento**:
```
IPFS:
  /projects/{projectId}/
    /milestones/{milestoneId}/
      evidence.json          # Metadata de evidencia
      photos/                # Fotos de avance
    /materials/{batchId}/
      certificate.pdf        # Certificado de calidad
      metadata.json          # Datos del material
    /documents/
      contract_hash.json     # Hash y metadata del contrato
      specs_hash.json        # Hash de EETT

Arweave:
  - Certificaciones de calidad finales
  - Contratos firmados (hash + metadata)
  - Actas de recepcion
```

### 3.4 Indexing (The Graph)

**Subgraphs custom**:

| Subgraph | Entidades | Queries Principales |
|----------|-----------|---------------------|
| milestone-payments | Project, Milestone, Payment, Dispute | Proyectos por cliente, pagos pendientes, historial |
| material-traceability | Material, Transfer, QualityCheck | Trazabilidad por lote, materiales por proyecto |
| quality-certifications | Certification, Project, Issuer | Certificaciones por proyecto, por tipo, por laboratorio |
| property-tokens | Property, Fraction, Investor, Distribution | Holdings por investor, historial de distribuciones |

**Ejemplo de schema (milestone-payments)**:
```graphql
type Project @entity {
  id: ID!
  client: Bytes!
  contractor: Bytes!
  totalAmount: BigInt!
  milestones: [Milestone!]! @derivedFrom(field: "project")
  status: ProjectStatus!
  createdAt: BigInt!
}

type Milestone @entity {
  id: ID!
  project: Project!
  description: String!
  amount: BigInt!
  deadline: BigInt!
  evidenceHash: Bytes
  status: MilestoneStatus!
  completedAt: BigInt
  payments: [Payment!]! @derivedFrom(field: "milestone")
}

type Payment @entity {
  id: ID!
  milestone: Milestone!
  amount: BigInt!
  recipient: Bytes!
  timestamp: BigInt!
  txHash: Bytes!
}

enum ProjectStatus { Active, Completed, Disputed, Cancelled }
enum MilestoneStatus { Pending, Submitted, Approved, Paid, Disputed }
```

### 3.5 Frontend Web3

**Stack**:

| Componente | Tecnologia | Proposito |
|------------|-----------|-----------|
| Framework | Next.js 14 (App Router) | SSR, routing, API routes |
| Web3 hooks | wagmi v2 | React hooks para Ethereum |
| Wallet connection | RainbowKit | Modal de conexion de wallets |
| Contract interaction | viem | TypeScript-first Ethereum client |
| Subgraph queries | Apollo Client / urql | Queries a The Graph |
| State management | Zustand | Estado global de la app |
| UI | shadcn/ui + Tailwind CSS | Componentes de interfaz |
| Forms | React Hook Form + Zod | Validacion de formularios |

**Wallets soportadas** (via RainbowKit):
- MetaMask (desktop + mobile)
- WalletConnect v2 (mobile wallets)
- Coinbase Wallet
- Rainbow
- Rabby

---

## 4. Integration Patterns

### 4.1 Oracle Pattern (Off-chain -> On-chain)

**Problema**: datos del mundo real (avance de obra, sensores IoT, clima) necesitan registrarse on-chain para activar logica de smart contracts.

**Solucion**:

```
[Datos Off-chain]
    |
    +---> IoT Sensors (temperatura, humedad, vibracion)
    +---> Project Management (avance, milestones)
    +---> Camaras (fotos de avance)
    +---> Laboratorios (resultados de ensayos)
    |
    v
[Oracle Service (Backend - FastAPI)]
    |
    +---> Validacion de datos (schema, rangos, autenticidad)
    +---> Firma digital del operador autorizado
    +---> Batch processing (agrupar multiples datos en una tx)
    |
    v
[Smart Contract]
    |
    +---> Verificar firma del oracle autorizado
    +---> Registrar dato on-chain
    +---> Ejecutar logica (liberar pago, emitir certificado, etc.)
    +---> Emitir evento
```

**Seguridad del oracle**:
- Multi-oracle: minimo 2 fuentes independientes para datos criticos
- Threshold: dato se acepta solo si N de M oracles coinciden
- Timelock: delay entre registro y ejecucion para permitir disputas
- Rate limiting: maximo N registros por periodo por oracle
- Key rotation: rotacion periodica de signing keys

### 4.2 Event-Driven Pattern

**Flujo: Smart Contract Events -> Backend -> Notificaciones**

```
[Smart Contract emite evento]
    |
    v
[Alchemy Webhooks / The Graph]
    |
    v
[Backend Webhook Handler (FastAPI)]
    |
    +---> Guardar en base de datos
    +---> Actualizar dashboard
    +---> Notificar stakeholders:
    |       +---> Email (SendGrid)
    |       +---> Push notification
    |       +---> Slack/WhatsApp
    |       +---> SMS (Twilio)
    |
    v
[Dashboard actualizado en real-time (WebSocket)]
```

**Eventos monitoreados**:

| Evento | Contrato | Accion Backend |
|--------|----------|----------------|
| ProjectCreated | ProjectRegistry | Crear proyecto en DB, notificar equipo |
| MilestoneSubmitted | MilestonePayment | Notificar aprobadores, iniciar timer |
| MilestoneApproved | MilestonePayment | Notificar contratista, preparar pago |
| PaymentClaimed | MilestonePayment | Registrar pago, actualizar contabilidad |
| MaterialShipped | MaterialTraceability | Notificar bodeguero, actualizar tracking |
| MaterialReceived | MaterialTraceability | Confirmar recepcion, actualizar inventario |
| CertificationIssued | QualityCertification | Agregar a expediente del proyecto |
| FractionPurchased | TokenizedProperty | Actualizar cap table, notificar investor |

### 4.3 Hybrid Storage Pattern

**Principio**: datos criticos e inmutables on-chain, datos voluminosos off-chain con verificacion on-chain.

```
[Dato completo (ej: reporte de avance con fotos)]
    |
    +---> Almacenar en IPFS (fotos, PDF, metadata JSON)
    |       Output: IPFS CID (content hash)
    |
    +---> Registrar on-chain:
            - IPFS CID (hash del contenido)
            - Timestamp
            - Autor (wallet address)
            - Tipo de documento
            - Project ID

[Verificacion]:
    1. Obtener CID del smart contract
    2. Obtener contenido de IPFS usando CID
    3. Hash del contenido obtenido == CID on-chain? -> Verificado
    4. Si no coincide -> contenido fue alterado
```

**Que va on-chain vs off-chain**:

| On-chain | Off-chain (IPFS/Arweave) | Off-chain (Database) |
|----------|--------------------------|----------------------|
| Hashes de documentos | Documentos completos | Metadata de busqueda |
| Estado de milestones | Evidencia fotografica | Historial de queries |
| Ownership de tokens | Metadata de NFTs | Cache de datos |
| Pagos y transfers | Certificados PDF | Analytics y reportes |
| Roles y permisos | Modelos 3D/BIM | Logs de aplicacion |

---

## 5. Security Practices

### 5.1 Pre-Deployment Checklist

**Codigo**:
- [ ] Todos los tests pasan (unit, integration, fuzz)
- [ ] Coverage >= 95%
- [ ] Slither: 0 high/medium findings
- [ ] Mythril: 0 high findings
- [ ] Peer review completado por minimo 2 developers
- [ ] Natspec documentation completa para funciones publicas

**Configuracion**:
- [ ] Constructor parameters verificados
- [ ] Admin roles asignados a multi-sig (Gnosis Safe)
- [ ] Pausable: owner es multi-sig
- [ ] Upgrade: UUPS con timelock
- [ ] Gas limits: verificados en condiciones de congestion

**Deployment**:
- [ ] Script de deployment testeado en fork de mainnet
- [ ] Verificacion de contrato en block explorer (Etherscan/Polygonscan)
- [ ] Documentacion de deployment: addresses, tx hashes, ABI
- [ ] Monitoring configurado: eventos, balances, transacciones fallidas

### 5.2 Gas Optimization Techniques

| Tecnica | Ahorro Estimado | Descripcion |
|---------|-----------------|-------------|
| Storage packing | 20-50% en writes | Agrupar variables < 256 bits en un slot |
| calldata vs memory | 10-30% en inputs | Usar calldata para parametros que no se modifican |
| Mappings vs arrays | Variable | Mappings para lookups, arrays solo si se necesita iteracion |
| Eventos vs storage | 80-90% | Usar eventos para datos que solo necesitan ser leidos off-chain |
| Batch operations | 30-60% | Agrupar multiples operaciones en una transaccion |
| Unchecked math | 5-15% | Solo donde overflow es imposible (ej: loop counters) |
| Short-circuit | Variable | Condiciones mas probables primero en require/if |
| Custom errors | 10-20% vs strings | Usar custom errors en vez de require con string |

### 5.3 Emergency Pause Mechanism

**Implementacion**:
```solidity
// Roles para emergency pause
bytes32 public constant PAUSER_ROLE = keccak256("PAUSER_ROLE");
bytes32 public constant UNPAUSER_ROLE = keccak256("UNPAUSER_ROLE");

// PAUSER_ROLE: puede ser un EOA para respuesta rapida
// UNPAUSER_ROLE: debe ser multi-sig (Gnosis Safe) con timelock

// Funciones criticas tienen modifier whenNotPaused
function claimPayment(...) external whenNotPaused nonReentrant { ... }
function transferMaterial(...) external whenNotPaused { ... }
```

**Protocolo de emergencia**:
1. Detectar incidente (monitoring automatico o reporte manual)
2. PAUSER ejecuta pause() - efecto inmediato
3. Investigar causa raiz
4. Desarrollar fix (nuevo contrato o update)
5. Testing del fix en fork
6. UNPAUSER (multi-sig) aprueba unpause o upgrade
7. Timelock period (24-48 horas)
8. Ejecutar unpause/upgrade
9. Post-mortem documentado

### 5.4 Upgrade Procedures (UUPS)

**Proceso de upgrade**:
```
1. Desarrollar nueva implementacion
    |
    v
2. Testing completo (mismos tests + nuevos)
    |
    v
3. Verificar storage layout compatible:
    - No reordenar variables existentes
    - Solo agregar nuevas variables al final
    - No cambiar tipos de variables existentes
    |
    v
4. Deploy nueva implementacion (no afecta proxy)
    |
    v
5. Proponer upgrade via multi-sig (Gnosis Safe)
    |
    v
6. Timelock period (48 horas minimo)
    |
    v
7. Multi-sig ejecuta upgradeToAndCall()
    |
    v
8. Verificar nueva implementacion en block explorer
    |
    v
9. Ejecutar tests de smoke en mainnet
    |
    v
10. Documentar: nueva address, ABI, cambios
```

**Storage layout verification**:
- Usar OpenZeppelin Upgrades Plugin para Hardhat
- Plugin verifica automaticamente compatibilidad de storage
- Mantener archivo `.openzeppelin/` en version control

---

## 6. Regulatory Compliance (Chile)

### 6.1 CMF (Comision para el Mercado Financiero)

**Clasificacion de tokens**:

| Tipo de Token | Clasificacion CMF | Requisitos |
|---------------|-------------------|------------|
| Utility Token (acceso a servicios MBC) | No regulado (actualmente) | Monitorear regulacion en desarrollo |
| Payment Token (stablecoins) | Regulado bajo Ley Fintech (2023) | Registro en CMF, requisitos de capital |
| Security Token (propiedad fraccionada) | Valor segun Ley 18.045 | Registro de emision, prospectos, intermediarios registrados |

**Ley Fintech (Ley 21.521)**:
- Registro obligatorio para plataformas de crowdfunding
- Requisitos de capital minimo
- Obligaciones de informacion al inversionista
- Limites de inversion por persona
- MBC debe evaluar si TokenizedProperty.sol califica como crowdfunding

### 6.2 KYC/AML

**Proceso de KYC para tokenizacion**:
1. Recoleccion de datos: nombre, RUT, domicilio, fuente de fondos
2. Verificacion de identidad: documento de identidad + selfie (via proveedor KYC)
3. Screening: PEP (Personas Expuestas Politicamente), listas de sanciones
4. Aprobacion: manual o automatica segun riesgo
5. Whitelisting: agregar wallet a whitelist on-chain
6. Monitoreo continuo: transacciones inusuales

**Proveedores KYC evaluados**:
- Sumsub: KYC/AML completo, soporte LATAM
- Onfido: verificacion de documentos con AI
- Metamap (ex Mati): fuerte presencia en LATAM, integracion con fuentes locales

**On-chain whitelist**:
```solidity
// Solo wallets verificadas pueden recibir tokens de propiedad
mapping(address => bool) public whitelist;

modifier onlyWhitelisted(address account) {
    require(whitelist[account], "Account not whitelisted");
    _;
}

function transfer(address to, uint256 amount)
    public
    onlyWhitelisted(msg.sender)
    onlyWhitelisted(to)
{
    // transfer logic
}
```

### 6.3 Data Protection

**Ley 19.628 (Proteccion de Datos Personales)**:
- Datos personales no se almacenan on-chain (solo wallet addresses)
- Mapping wallet <-> identidad almacenado off-chain (base de datos encriptada)
- Derecho a cancelacion: se puede revocar whitelist y eliminar datos off-chain
- Consentimiento explicito para procesamiento de datos

**Preparacion para nueva ley de datos** (en tramitacion al 2026):
- Designar DPO (Data Protection Officer)
- Registro de bases de datos ante autoridad
- Evaluacion de impacto en proteccion de datos (EIPD)
- Procedimientos de breach notification

### 6.4 Tributacion

**Aspectos tributarios de tokens**:
- Venta de tokens: potencial hecho gravado con IVA (evaluar caso a caso)
- Ganancias de capital en tokens: tributacion segun regimen general (Art. 17 LIR)
- Distribucion de arriendos via tokens: retencion de impuesto a la renta
- Documentacion: emision de factura o boleta segun corresponda
- **Recomendacion**: contar con asesoria tributaria especializada para cada proyecto de tokenizacion

---

## 7. Roadmap Blockchain 2026

| Fase | Timeline | Entregables |
|------|----------|-------------|
| **Foundation** | Q1 2026 | Smart contracts en testnet, testing completo, documentacion |
| **Pilot** | Q2 2026 | Deploy en Polygon Amoy con 1 proyecto piloto, frontend basico |
| **Production v1** | Q3 2026 | MilestonePayment + MaterialTraceability en Polygon mainnet |
| **Expansion** | Q4 2026 | QualityCertification + ProjectRegistry, The Graph subgraphs |
| **Tokenization** | 2027 | Evaluacion regulatoria de TokenizedProperty, sandbox CMF |

---

*Este documento se actualiza con cada deploy de contrato o cambio de arquitectura. Responsable: Blockchain Lead.*

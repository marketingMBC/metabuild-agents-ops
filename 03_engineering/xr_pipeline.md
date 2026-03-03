# Pipeline de Produccion XR

> Documento de referencia para la produccion de experiencias XR en Meta Build City.
> Aplica a: recorridos virtuales, VR training, AR overlays, WebXR experiences.
> Ultima actualizacion: Febrero 2026

---

## 1. Pre-Produccion

### 1.1 Briefing con Cliente

**Duracion estimada**: 1-2 reuniones (1-2 horas cada una)

**Inputs requeridos del cliente**:
- Objetivos del proyecto (venta, capacitacion, marketing, coordinacion)
- Assets disponibles: planos CAD/BIM, modelos 3D, renders, fotos de referencia
- Publico objetivo: compradores, obreros, ingenieros, inversionistas
- Plataforma deseada: VR headset, web, mobile, desktop
- Presupuesto y timeline
- Restricciones tecnicas: ancho de banda, dispositivos del usuario final

**Outputs**:
- Brief documentado en Notion
- Scope of Work (SoW) preliminar
- Lista de assets a recibir/crear

### 1.2 Asset Gathering

**Checklist de assets**:

| Tipo | Formato Preferido | Alternativas | Notas |
|------|-------------------|--------------|-------|
| Modelos BIM | .rvt (Revit) | .ifc, .nwc | Incluir familias y materiales |
| Modelos 3D | .fbx | .obj, .glb, .3ds | Con UVs y materiales asignados |
| Texturas | .png / .jpg | .tga, .exr | Resolucion minima 2048x2048 para PBR |
| Planos 2D | .dwg | .pdf, .dxf | Acotados, con escalas |
| Fotos referencia | .jpg / .png | - | Materiales reales, acabados, entorno |
| Branding | .ai / .svg | .png (alta res) | Logos, colores corporativos, tipografias |
| Documentacion | .pdf / .docx | - | Especificaciones tecnicas, fichas de producto |

**Proceso de recepcion**:
1. Cliente sube assets a carpeta compartida (Google Drive / ACC)
2. Asset manager revisa completitud y calidad
3. Se genera reporte de gaps y solicitudes adicionales
4. Assets se organizan en estructura estandar del proyecto

### 1.3 Storyboard / User Flow

**Para recorridos virtuales**:
- Mapa de navegacion: puntos de interes, rutas, transiciones
- Wireframes de UI: menus, info panels, controles
- Script de guided tour (si aplica)
- Definicion de interactive hotspots

**Para VR training**:
- Scenario flowchart: decision trees, branching paths
- Definicion de evaluacion: criterios de aprobacion/reprobacion
- Guion de instrucciones y feedback

**Para AR overlays**:
- Definicion de layers de informacion
- Mapping de coordenadas BIM a coordenadas reales
- User flow de campo: como el inspector usa la app en obra

**Herramientas**: Miro (flowcharts), Figma (UI wireframes), Google Docs (scripts)

### 1.4 Technical Assessment

**Evaluacion de plataforma target**:

| Plataforma | GPU Budget | Poly Count Max | Texture Budget | Draw Calls Max |
|------------|-----------|----------------|----------------|----------------|
| Meta Quest 3 | Mobile GPU | 500K-1M tris | 512MB VRAM | <200 |
| Web (Three.js) | Varies | 200K-500K tris | 100MB total download | <150 |
| Desktop VR | Desktop GPU | 2M-5M tris | 2GB VRAM | <500 |
| Mobile AR | Mobile GPU | 100K-300K tris | 256MB VRAM | <100 |
| Pixel Streaming | Server GPU | 5M+ tris | 4GB+ VRAM | <1000 |

**Decisiones tecnicas**:
- Engine: Unity vs Unreal (basado en requerimientos de fidelidad y plataforma)
- Rendering: real-time vs pre-baked lighting
- Networking: single-user vs multi-user
- Audio: spatial audio requirements
- Localization: idiomas requeridos

### 1.5 Production Plan

**Template de plan**:

```
Proyecto: [Nombre]
Cliente: [Cliente]
Tipo: [Recorrido Virtual / VR Training / AR Overlay]
Engine: [Unity / Unreal / WebXR]
Plataforma: [Quest / Web / Desktop / Mobile]
Timeline: [X semanas]
Equipo:
  - Tech Lead: [nombre]
  - 3D Artist: [nombre]
  - Developer: [nombre]
  - QA: [nombre]

Milestones:
  - M1 (Semana X): Graybox / blockout aprobado
  - M2 (Semana X): Art pass completo
  - M3 (Semana X): Interacciones implementadas
  - M4 (Semana X): QA interno completo
  - M5 (Semana X): Client UAT y ajustes
  - M6 (Semana X): Delivery final
```

---

## 2. Produccion - Recorridos Virtuales

### 2.1 Model Preparation

**Pipeline de importacion BIM/CAD a real-time**:

```
Revit/ArchiCAD (.rvt/.pln)
    |
    v
Export a FBX / IFC
    |
    v
Import a Blender
    |
    v
Cleanup y Optimization:
    - Eliminar geometria oculta/innecesaria
    - Merge de objetos por material
    - Reducir polycount (Decimate modifier si necesario)
    - Corregir normals
    - Unwrap UVs para lightmapping
    |
    v
Export a formato del engine (.fbx)
    |
    v
Import al engine (Unity/Unreal)
    |
    v
Material assignment y ajustes
```

**Reglas de optimizacion**:
- **Polycount**: reducir a <30% del modelo BIM original sin perder siluetas
- **Materiales**: consolidar materiales similares (max 50-100 materiales unicos)
- **Texturas**: texture atlasing para reducir draw calls
- **Instancing**: usar instancias para objetos repetidos (puertas, ventanas, muebles)
- **LODs**: generar 3 niveles de detalle (LOD0: full, LOD1: 50%, LOD2: 25%)

### 2.2 Environment Setup

**Iluminacion**:
- **Baked lighting** (preferido para recorridos): Lightmass (Unreal) o Progressive Lightmapper (Unity)
- **Mixed lighting**: luces puntuales dinamicas para interactividad (encender/apagar)
- **Reflection probes**: posicionar en cada habitacion para reflejos realistas
- **Light probes**: grid de probes para iluminacion indirecta en objetos dinamicos

**Materiales PBR**:
- Base Color, Normal Map, Metallic, Roughness, AO (minimo)
- Resolucion: 2048x2048 para superficies grandes, 1024x1024 para objetos menores
- Fuentes: Substance Source, Poly Haven, Quixel Megascans (Unreal), custom

**Post-processing**:
- Tone mapping, bloom, ambient occlusion (SSAO/HBAO)
- Color grading acorde a branding del proyecto
- Profundidad de campo (sutil, para evitar motion sickness en VR)

### 2.3 Interaction Design

**Tipos de navegacion**:

| Metodo | Plataforma | Descripcion |
|--------|-----------|-------------|
| Teleport | VR (Quest) | Click para moverse a puntos predefinidos |
| Free locomotion | VR (Quest) | Joystick para moverse libremente |
| Point-and-click | Desktop / Web | Click en suelo para moverse |
| Orbital | Desktop / Web | Rotar alrededor del modelo (exterior) |
| Auto-guided tour | Todas | Recorrido automatico con narration |

**Hotspots interactivos**:
- Info panels: fichas tecnicas de materiales, dimensiones, precios
- Media: fotos, videos, renders de terminaciones alternativas
- Configuradores: cambiar materiales (pisos, muros, mesones) en real-time
- Vistas: comparar dia/noche, amoblado/sin amoblar

### 2.4 UI/UX

**Principios de UI en VR/XR**:
- Texto legible a distancia (minimo 24pt equivalent en VR)
- Contraste alto (WCAG AA minimo)
- Feedback visual y haptico en interacciones
- Menu principal accesible en todo momento (wrist menu en VR)
- Minimizar motion sickness: vignette en movimiento, snap turn

**Elementos estandar de UI**:
- Menu principal: seleccion de departamento/piso
- Minimap: ubicacion actual en el recorrido
- Info panel: ficha del proyecto, contacto
- Settings: calidad grafica, idioma, confort settings
- Screenshot/video: captura de vistas favoritas

### 2.5 Performance Optimization

**Checklist de optimizacion**:

| Tecnica | Descripcion | Impacto |
|---------|-------------|---------|
| Occlusion Culling | No renderizar objetos ocultos por paredes | Alto |
| LOD (Level of Detail) | Reducir detalle en objetos lejanos | Alto |
| Texture Atlasing | Combinar texturas en una sola sheet | Medio |
| Static Batching | Combinar meshes estaticos | Medio |
| GPU Instancing | Renderizar copias de objetos en un draw call | Medio |
| Lightmap Resolution | Ajustar resolucion de lightmaps por importancia | Medio |
| Mesh Compression | Reducir tamano de archivos de mesh | Bajo |
| Audio Compression | Comprimir audio sin perder calidad perceptible | Bajo |

**Profiling**:
- Unity: Profiler window, Frame Debugger, Memory Profiler
- Unreal: Stat commands, Unreal Insights, GPU Visualizer
- Quest: OVR Metrics Tool, Meta Quest Developer Hub
- Web: Chrome DevTools Performance tab, Three.js stats

### 2.6 Cross-Platform Build

**Build matrix**:

| Plataforma | Engine | Build Target | Distribucion |
|------------|--------|-------------|--------------|
| Meta Quest 3 | Unity / Unreal | Android (APK/AAB) | Meta App Lab / sideload |
| Web | Unity (WebGL) / Three.js | HTML5 | Hosting propio (Vercel/S3) |
| Desktop VR | Unreal / Unity | Windows (SteamVR/OpenXR) | Installer / Steam |
| iOS AR | Unity (AR Foundation) | iOS | TestFlight / App Store |
| Android AR | Unity (AR Foundation) | Android | APK / Play Store |
| Pixel Streaming | Unreal | Windows Server | AWS EC2 + web client |

**Quality settings por plataforma**:
- Quest: Medium quality, baked lighting, 72-120 FPS target
- Web: Low-Medium quality, compressed textures, 60 FPS target
- Desktop VR: High-Ultra quality, ray tracing (optional), 90 FPS target
- Pixel Streaming: Ultra quality, renderizado en servidor, latencia <50ms

---

## 3. Produccion - VR Training

### 3.1 Scenario Design

**Tipos de escenarios para construccion**:

| Categoria | Ejemplos | Interacciones Clave |
|-----------|----------|---------------------|
| Seguridad | Caida de altura, contacto electrico, derrumbe | Identificar riesgos, aplicar procedimiento |
| Operacion de equipos | Grua torre, retroexcavadora, montacargas | Operar controles, seguir checklist |
| Procedimientos | Hormigonado, soldadura, instalacion electrica | Seguir secuencia correcta de pasos |
| Emergencia | Incendio, sismo, accidente | Evacuacion, primeros auxilios, comunicacion |

**Estructura de escenario**:
1. **Briefing**: introduccion al contexto, objetivos de aprendizaje
2. **Exploracion**: familiarizacion con el entorno virtual
3. **Tarea guiada**: paso a paso con indicaciones
4. **Tarea autonoma**: sin ayuda, evaluado
5. **Debrief**: feedback, puntuacion, areas de mejora

### 3.2 Character & Environment Creation

**Personajes**:
- Modelos 3D humanoides con animaciones: idle, walk, talk, work, fall, injury
- Rigging: humanoid rig compatible con Mixamo / custom
- Customizacion: casco, chaleco, guantes, lentes (EPP variado)
- Lip sync: basico para instrucciones narradas

**Entornos**:
- Obra gruesa: estructura de hormigon, moldajes, fierros
- Obra de terminaciones: tabiqueria, instalaciones, acabados
- Exterior: terreno, maquinaria, accesos, zonas de acopio
- Basados en tipologias reales de proyectos chilenos

### 3.3 Interaction Mechanics

**Interacciones de mano en VR**:

| Accion | Implementacion | Uso |
|--------|---------------|-----|
| Grab | Physics-based grab (XR Interaction Toolkit) | Tomar herramientas, materiales, EPP |
| Inspect | Rotar objeto frente a la cara | Revisar estado de materiales, leer etiquetas |
| Activate | Button press / trigger pull | Operar herramientas, presionar botones |
| Point | Ray interactor | Senalar riesgos, seleccionar opciones de menu |
| Two-hand | Dual grab | Operar herramientas grandes, abrir planos |

**Feedback al usuario**:
- Visual: highlights, arrows, particle effects
- Audio: instrucciones narradas, sonidos de alerta, confirmacion
- Haptico: vibracion de controllers en interacciones y alertas

### 3.4 Scoring / Assessment System

**Metricas evaluadas**:

| Metrica | Peso | Descripcion |
|---------|------|-------------|
| Completitud | 30% | Pasos completados correctamente / total de pasos |
| Tiempo | 20% | Tiempo de ejecucion vs tiempo objetivo |
| Errores criticos | 25% | Acciones que causarian accidente (fail automatico si >0) |
| Errores menores | 15% | Acciones incorrectas pero no criticas |
| EPP | 10% | Uso correcto de equipo de proteccion personal |

**Sistema de puntuacion**:
- 90-100%: Aprobado con distincion
- 70-89%: Aprobado
- 50-69%: Requiere refuerzo
- <50%: Reprobado, debe repetir

**Generacion de reportes**:
- PDF automatico con resultados por usuario
- Dashboard con metricas agregadas por grupo/empresa
- Exportacion a LMS del cliente (SCORM 2004 si requerido)

### 3.5 Analytics Integration

**Datos capturados**:
- Evento por evento: timestamp, accion, resultado, posicion del usuario
- Heatmaps: donde mira y donde se mueve el usuario
- Time-on-task por paso
- Patrones de error: errores frecuentes por escenario

**Pipeline de datos**:
```
VR App (Unity/Unreal)
    |
    v
Event Logger (JSON)
    |
    v
API Endpoint (FastAPI)
    |
    v
Database (PostgreSQL)
    |
    v
Dashboard (Metabase / custom Next.js)
```

### 3.6 Multi-Language Support

**Idiomas soportados**: Espanol (Chile), Espanol (neutro), Ingles, Portugues (Brasil)

**Implementacion**:
- Texto UI: sistema de localizacion del engine (Unity Localization / Unreal Text Localization)
- Audio narrado: archivos de audio separados por idioma
- Senaletica 3D: texturas intercambiables
- Selector de idioma en menu principal

---

## 4. Produccion - AR Overlays

### 4.1 Marker / Anchor Definition

**Metodos de anclaje**:

| Metodo | Precision | Requisitos | Uso |
|--------|-----------|------------|-----|
| QR Code markers | Alta (cm) | Imprimir y posicionar QR en obra | Puntos fijos de referencia |
| GPS + compass | Baja (metros) | Ubicacion exterior | Posicionamiento inicial grueso |
| LiDAR scan matching | Alta (cm) | iPhone/iPad Pro con LiDAR | Alineacion automatica con escaneo previo |
| BIM coordinates | Alta (mm) | Estacion total o puntos de referencia | Alineacion precisa con modelo BIM |
| Visual markers (SLAM) | Media (cm-dm) | Camara del dispositivo | Tracking continuo del entorno |

**Proceso de calibracion BIM-to-reality**:
1. Obtener coordenadas de referencia del modelo BIM (minimo 3 puntos)
2. Medir mismos puntos en obra con estacion total o LiDAR
3. Calcular transformacion (rotacion, traslacion, escala)
4. Aplicar transformacion al modelo AR
5. Validar alineacion visualmente en campo
6. Ajustar fino si es necesario

### 4.2 3D Overlay Creation

**Capas de informacion AR**:

| Capa | Color Standard | Contenido |
|------|---------------|-----------|
| Estructura | Gris/Azul | Pilares, vigas, losas, muros estructurales |
| Agua potable | Verde | Tuberias de agua fria y caliente |
| Alcantarillado | Marron | Bajadas, colectores, camaras |
| Electrico | Amarillo | Canalizaciones, tableros, puntos |
| Gas | Rojo | Tuberias de gas, reguladores |
| HVAC | Cyan | Ductos, equipos de climatizacion |
| Incendio | Rojo oscuro | Red humeda, rociadores, detectores |

**Visualizacion**:
- Wireframe: para ver a traves del overlay
- X-ray: semi-transparente para ver instalaciones detras de muros
- Highlighted: resaltar un sistema especifico, ocultar los demas
- Clash: mostrar interferencias detectadas en rojo parpadeante

### 4.3 Information Layers

**Datos mostrados al usuario en AR**:

| Tipo de Dato | Fuente | Interaccion |
|--------------|--------|-------------|
| Dimensiones | Modelo BIM | Tap en elemento para ver medidas |
| Especificaciones | Base de datos MBC | Ficha tecnica del material/equipo |
| Estado de avance | Sistema de gestion de obra | Porcentaje completado, color coding |
| Observaciones | BIMcollab / campo | Issues pendientes con foto y descripcion |
| Historial | Logs del proyecto | Timeline de cambios en el elemento |
| Responsable | Planificacion | Subcontratista/cuadrilla asignada |

### 4.4 Camera / Sensor Calibration

**Proceso de calibracion por dispositivo**:

| Dispositivo | Calibracion | Frecuencia |
|-------------|-------------|------------|
| iPhone/iPad Pro | Automatica (ARKit) | Cada sesion |
| HoloLens 2 | Eye tracking + spatial mapping | Primera vez + recalibracion mensual |
| Android (ARCore) | Automatica | Cada sesion |
| Custom cameras | Calibracion manual (OpenCV checkerboard) | Cada instalacion |

**Consideraciones de campo**:
- Iluminacion: funciona mejor con luz natural. Evitar contraluz directo.
- Superficies: el tracking falla en superficies reflectantes o sin textura.
- Polvo/suciedad: limpiar lente del dispositivo antes de usar.
- Vibracion: evitar usar durante operacion de maquinaria pesada cercana.

### 4.5 Field Testing and Adjustment

**Protocolo de testing en obra**:

1. **Pre-test** (oficina):
   - Verificar modelo cargado correctamente
   - Probar en espacio controlado con medidas conocidas
   - Verificar conectividad (WiFi/4G en obra)

2. **Test en campo** (primera visita):
   - Calibrar puntos de referencia
   - Verificar alineacion BIM-realidad en multiples zonas
   - Documentar desfases (fotos + medidas)
   - Probar con usuarios finales (ingeniero de terreno)

3. **Ajustes**:
   - Corregir transformacion de coordenadas
   - Ajustar escala si es necesario
   - Actualizar modelo con cambios de obra

4. **Validacion**:
   - Re-test con ajustes aplicados
   - Sign-off del ingeniero de terreno
   - Documentar precision lograda

---

## 5. Post-Produccion

### 5.1 QA Testing

**QA Checklist por plataforma**:

**General (todas las plataformas)**:
- [ ] Todas las interacciones funcionan correctamente
- [ ] Textos sin errores ortograficos
- [ ] Audio reproduce correctamente
- [ ] UI responsive a diferentes resoluciones
- [ ] No hay assets faltantes (texturas rosadas, meshes invisibles)
- [ ] Transiciones suaves entre escenas/areas

**VR (Quest)**:
- [ ] Frame rate estable >= 72 FPS
- [ ] Sin judder ni flickering
- [ ] Controllers trackeados correctamente
- [ ] Guardian system no interfiere con la experiencia
- [ ] Comfort settings funcionan (vignette, snap turn)
- [ ] No produce motion sickness en sesiones de 15+ minutos

**Web**:
- [ ] Carga en <10 segundos (conexion de 10 Mbps)
- [ ] Funciona en Chrome, Firefox, Safari, Edge
- [ ] Responsive (desktop, tablet, mobile)
- [ ] Touch controls funcionan en mobile
- [ ] Performance estable (60 FPS en hardware medio)

**AR**:
- [ ] Tracking estable en condiciones de obra
- [ ] Alineacion precisa con realidad (<5cm de error)
- [ ] Funciona con iluminacion variable
- [ ] No crash en sesiones de 30+ minutos
- [ ] Datos se actualizan correctamente

### 5.2 Client Review

**Proceso de revision iterativa**:

| Fase | Entrega | Feedback Esperado |
|------|---------|-------------------|
| Alpha | Build funcional, arte placeholder | Flujo correcto, navegacion, interacciones |
| Beta | Arte final, features completas | Ajustes esteticos, contenido, branding |
| RC (Release Candidate) | Build casi final | Bugs menores, pulido final |
| Gold | Build final aprobado | Sign-off formal |

**Herramientas de feedback**:
- Sesion en vivo (Zoom/presencial) con screen share o co-presencia en VR
- Formulario de feedback estructurado (Google Forms / Notion)
- Video grabado del recorrido con comentarios
- Bug tracker (Linear) para issues especificos

### 5.3 Deployment

**Matriz de deployment**:

| Plataforma | Metodo de Distribucion | Update Process |
|------------|----------------------|----------------|
| Quest (App Lab) | Upload a Meta App Lab, review process | OTA update via store |
| Quest (sideload) | APK via SideQuest o ADB | Manual reinstall |
| Web | Deploy a Vercel/S3 + CloudFront | CI/CD push to production |
| Desktop | Installer (NSIS/InnoSetup) o Steam | Auto-update o manual download |
| iOS | TestFlight (beta) / App Store (prod) | Store update |
| Pixel Streaming | EC2 instance + web client | Server redeploy |

### 5.4 Training del Equipo del Cliente

**Contenido del training**:
- Uso basico de la experiencia XR
- Troubleshooting comun (device setup, connectivity)
- Como actualizar contenido (si aplica)
- Como interpretar analytics/reportes
- Contacto de soporte MBC

**Formato**:
- Sesion presencial (2-4 horas)
- Video tutorial grabado
- Manual de usuario (PDF)
- FAQ document

### 5.5 Handoff

**Paquete de entrega**:

```
/proyecto-[nombre]/
  /builds/
    quest/         # APK + instrucciones de instalacion
    web/           # Build web lista para deploy
    desktop/       # Installer o ejecutable
  /source/
    unity-project/ # O unreal-project/ - proyecto completo
    assets/        # Assets originales (Blender, Substance, etc.)
  /docs/
    README.md              # Overview del proyecto
    architecture.md        # Arquitectura tecnica
    deployment-guide.md    # Como desplegar/actualizar
    user-manual.pdf        # Manual de usuario final
    maintenance-guide.md   # Guia de mantenimiento
  /analytics/
    dashboard-setup.md     # Como acceder a analytics
    data-schema.md         # Estructura de datos capturados
```

---

## 6. Quality Standards

### Performance Targets

| Plataforma | Frame Rate | Load Time | File Size Max | Latencia (streaming) |
|------------|-----------|-----------|---------------|----------------------|
| Meta Quest 3 | >= 72 FPS (ideal 90) | < 15 sec | 2 GB (APK) | N/A |
| Web (desktop) | >= 60 FPS | < 10 sec | 100 MB (initial load) | N/A |
| Web (mobile) | >= 30 FPS | < 15 sec | 50 MB (initial load) | N/A |
| Desktop VR | >= 90 FPS | < 10 sec | 10 GB | N/A |
| Pixel Streaming | >= 60 FPS | < 5 sec (stream start) | N/A (server-side) | < 50 ms |
| AR (mobile) | >= 30 FPS | < 10 sec | 500 MB | N/A |

### Visual Quality Standards

- **Lightmap resolution**: minimo 10 texels/meter para superficies principales
- **Texture resolution**: minimo 1024x1024 para materiales visibles de cerca
- **Anti-aliasing**: MSAA 4x (Quest), TAA (desktop), FXAA (web)
- **Shadow quality**: soft shadows en todas las plataformas excepto mobile web

### Accessibility Standards

| Feature | Implementacion |
|---------|---------------|
| Comfort settings | Vignette, snap turn, seated mode |
| Text size | Ajustable, minimo legible sin esfuerzo |
| Audio descriptions | Narracion de elementos visuales importantes |
| Color blind modes | Paleta alternativa para informacion color-coded |
| Subtitles | Para todo audio narrado |
| One-hand mode | Navegacion posible con un solo controller |

---

## 7. Tools per Stage

### Matriz de Herramientas por Etapa

| Etapa | Herramientas Principales | Herramientas de Soporte |
|-------|--------------------------|------------------------|
| **Briefing** | Notion, Miro, Google Meet | Google Docs, Loom |
| **Asset Gathering** | Google Drive, ACC, Speckle | WeTransfer (archivos grandes) |
| **Storyboard** | Miro, Figma | Canva, Google Slides |
| **Tech Assessment** | Notion (template), Spreadsheets | Device testing lab |
| **Model Prep** | Blender, 3ds Max, SketchUp | Substance Painter, Polyhaven |
| **Environment** | Unity / Unreal Engine | Substance Designer, Megascans |
| **Interactions** | Unity XR Toolkit / Unreal VR Template | Custom C#/C++ scripts |
| **UI/UX** | Figma (design), Unity UI / UMG (impl) | TextMeshPro, Canvas |
| **Optimization** | Profiler (Unity/Unreal), OVR Metrics | RenderDoc, PIX |
| **QA** | Linear (bugs), Notion (checklist) | Screen recording, OBS |
| **Deployment** | GitHub Actions, Docker | AWS CLI, Vercel CLI |
| **Analytics** | FastAPI, PostgreSQL, Metabase | Google Analytics (web) |
| **Training** | Zoom, Loom, Google Docs | Notion (knowledge base) |

---

## 8. Estimaciones de Tiempo por Tipo de Proyecto

### Recorrido Virtual Inmobiliario (departamento/casa)

| Fase | Duracion | Equipo |
|------|----------|--------|
| Pre-produccion | 1 semana | PM + Tech Lead |
| Produccion | 3-4 semanas | 3D Artist + Developer |
| QA + Client Review | 1 semana | QA + PM |
| Deployment + Handoff | 0.5 semanas | Developer + PM |
| **Total** | **5-6 semanas** | **3-4 personas** |

### VR Training Module (1 escenario)

| Fase | Duracion | Equipo |
|------|----------|--------|
| Pre-produccion | 2 semanas | PM + Tech Lead + SME |
| Produccion | 4-6 semanas | 3D Artist + Developer + Instructional Designer |
| QA + Client Review | 2 semanas | QA + PM + SME |
| Deployment + Handoff | 1 semana | Developer + PM |
| **Total** | **9-11 semanas** | **4-5 personas** |

### AR Overlay (edificio completo)

| Fase | Duracion | Equipo |
|------|----------|--------|
| Pre-produccion | 1-2 semanas | PM + Tech Lead + BIM Specialist |
| Produccion | 4-6 semanas | Developer + BIM Specialist |
| Field Testing | 2 semanas | Developer + Field Engineer |
| Deployment + Handoff | 1 semana | Developer + PM |
| **Total** | **8-11 semanas** | **3-4 personas** |

---

*Este pipeline se revisa y actualiza al cierre de cada proyecto con lecciones aprendidas. Responsable: XR Tech Lead.*

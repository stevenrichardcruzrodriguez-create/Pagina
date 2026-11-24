# 🏭 FÁBRICA DE SIMULADORES 3D · Plantilla Maestra v1.0
### Basada en el simulador "Motor de 4 Tiempos" · Estilo laboratorio educativo interactivo

> **Qué es este archivo:** una instrucción completa + código de referencia para que
> cualquier IA (Claude, ChatGPT, Gemini, Copilot…) construya un simulador 3D interactivo
> nuevo, sobre el tema que tú elijas, con la misma calidad, estructura y estilo visual
> del simulador del motor de gasolina de 4 tiempos.

---

## 1 · INSTRUCCIONES PARA LA PERSONA (léelo primero, toma 1 minuto)

1. **Edita SOLO el bloque de la sección 2** ("PETICIÓN DEL PROFESOR"). Lo único
   obligatorio es escribir el `TEMA`. Todo lo demás puedes dejarlo en `"auto"`.
2. **Copia TODO este archivo completo** (incluido el código de muestra del final)
   y pégalo como un único mensaje a la IA que uses.
3. La IA te responderá con **un solo archivo HTML**. Guárdalo como
   `mi-simulador.html` y ábrelo con doble clic en Chrome, Edge o Firefox.
   *Necesita internet la primera vez* (carga la librería 3D y las fuentes desde CDN).

**Si algo sale mal:**
- La IA cortó el código a la mitad → escríbele: *"continúa exactamente donde quedaste, sin repetir lo ya enviado"*.
- Pantalla de error al abrir → revisa la conexión a internet y recarga.
- Va lento en un equipo del aula → dentro del simulador, baja "Calidad gráfica" a **Baja**.
- ¿Quieres otro idioma? → cambia `IDIOMA` en la petición.

---

## 2 · ✏️ PETICIÓN DEL PROFESOR — EDITA SOLO ESTE BLOQUE

```yaml
# ======== RELLENA ESTO (solo TEMA es obligatorio) ========
TEMA: "ESCRIBE AQUÍ DE QUÉ QUIERES EL SIMULADOR"
ASIGNATURA: "auto"            # ej: "Biología · grado 7°"
EDAD_ESTUDIANTES: "11-15"
IDIOMA: "español"             # todo el simulador saldrá en este idioma
PARTES_CLAVE: "auto"          # lista de 8-15 piezas a rotular, o "auto" (la IA decide)
FENOMENO_A_ANIMAR: "auto"     # qué se mueve/cambia, o "auto"
FASES_DEL_PROCESO: "auto"     # 2-6 etapas para la línea de tiempo, o "auto"
COLOR_BASE: "auto"            # color dominante, o "auto" (la IA lo deriva del tema)
SONIDO: "si"                  # "si" o "no"
OBSERVACIONES: ""             # cualquier deseo extra
# ==========================================================
```

**Ejemplo ya rellenado (bórralo o reemplázalo por el tuyo):**

```yaml
TEMA: "El corazón humano: cámaras, válvulas y circulación de la sangre"
ASIGNATURA: "Biología · grado 7°"
EDAD_ESTUDIANTES: "12-14"
IDIOMA: "español"
PARTES_CLAVE: "aurícula derecha, aurícula izquierda, ventrículo derecho, ventrículo izquierdo, válvula mitral, válvula tricúspide, arteria aorta, arteria pulmonar, venas cavas, venas pulmonares, tabique"
FENOMENO_A_ANIMAR: "El ciclo cardíaco: llenado (diástole), contracción (sístole), apertura y cierre de válvulas, y flujo de sangre (azul = pobre en oxígeno, roja = rica en oxígeno)"
FASES_DEL_PROCESO: "1 Llenado · 2 Contracción auricular · 3 Sístole ventricular · 4 Relajación"
COLOR_BASE: "carmesí profundo con acentos azul venoso y rojo arterial"
SONIDO: "si, latido sincronizado con la sístole"
OBSERVACIONES: "El despiece debe separar las cámaras para poder ver las válvulas por dentro"
```

**Temas que funcionan espectacular con esta plantilla:**
el corazón humano · el sistema solar · un volcán en erupción · la célula animal o
vegetal · el átomo (modelo de Bohr) · el ciclo del agua · una turbina eólica · el ojo
humano · los pulmones y la respiración · la neurona y la sinapsis · placas tectónicas
y terremotos · un motor eléctrico · un circuito eléctrico · una bomba hidráulica ·
un cohete por etapas · la digestión · la fotosíntesis · un molino de agua.

---

## 3 · 🤖 INSTRUCCIONES PARA LA IA — NO EDITAR ESTA SECCIÓN

Eres un arquitecto frontend de élite, diseñador de producto, artista técnico 3D e
ingeniero de QA. Tu misión: construir un **simulador educativo 3D interactivo** sobre
el `TEMA` de la sección 2, dirigido a estudiantes de `EDAD_ESTUDIANTES`, en `IDIOMA`,
con la **misma huella visual, estructura y calidad** del código de muestra de la
sección 6. El código de muestra es la **referencia canónica**: reutiliza sus patrones,
helpers, CSS base y arquitectura, pero el contenido, la geometría, la cinemática, los
textos y la paleta deben ser del tema pedido. **El resultado nunca debe ser el motor
de 4 tiempos** (salvo que el TEMA lo pida explícitamente).

### 3.1 · Entrega
- **Un único archivo HTML completo y autocontenido**, ejecutable con doble clic
  (`file://`), sin build, sin servidor, sin frameworks, sin assets externos除了
  los CDN indicados. Sin TODOs, sin placeholders, sin handlers vacíos.
- Responde **solo** con el HTML completo en un bloque de código, más máximo
  4 viñetas de uso en `IDIOMA`. Si te cortas, continúa bajo petición sin reiniciar.

### 3.2 · Stack técnico obligatorio (idéntico al de la muestra)
- **Three.js r160** vía importmap + módulos ES desde jsDelivr:
  ```html
  <script type="importmap">
  { "imports": {
    "three": "https://cdn.jsdelivr.net/npm/three@0.160.0/build/three.module.js",
    "three/addons/": "https://cdn.jsdelivr.net/npm/three@0.160.0/examples/jsm/"
  } }
  </script>
  ```
  Addons: `OrbitControls`, `RoomEnvironment`, `EffectComposer`, `RenderPass`,
  `UnrealBloomPass`, `OutputPass`.
- **Google Fonts:** `Chakra Petch` (títulos, números, insignias) + `Inter` (cuerpo).
- Vanilla JS con **un solo** `renderer.setAnimationLoop`, un objeto `state` central,
  helpers (`$`, `clamp`, `lerp`, `easeIO`, `smooth`), `ResizeObserver`, pixel ratio
  limitado según calidad, `try/catch` en la carga con **pantalla de error amigable**
  en el idioma elegido + botón "Reintentar", y **loader animado** con el ícono del tema.

### 3.3 · Estructura de pantalla (obligatoria, espejo de la muestra)
- **Cabecera (~60px):** logo SVG animado del tema + título + subtítulo + chip con el
  concepto clave del fenómeno + botón de **SONIDO visible arriba** (estado actual,
  silencia todo con un clic, activado por defecto si `SONIDO: si`) + pantalla completa.
- **Escena 3D (izquierda):** fondo degradado con brillos radiales, niebla, polvo
  flotante, plataforma con anillo emisivo y pedestal; overlays: **insignia de fase
  actual** (número, nombre, color, animación pop), chip de ayuda, **ficha de pieza**
  (aparece al seleccionar), **línea de tiempo inferior** con las fases coloreadas,
  marcador de progreso, lecturas numéricas y marcas conceptuales (como PMS/PMI en el
  motor), capas de grano y viñeta.
- **Panel derecho permanente (~336px), nunca en modal**, con ≥7 herramientas vivas:
  1. Reproducir/Pausar · 2. Paso a paso (avanza una fase exacta) · 3. Deslizador de
  velocidad con unidades del tema · 4. **Botón DESPIECE** + deslizador de separación
  0–100% · 5. Toggle corte transversal (o rayos X si no hay interior) · 6. Toggle
  etiquetas · 7. Toggle giro automático · 8. Selector de calidad (Alta/Media/Baja) ·
  9. Presets de cámara (frontal, lateral, superior, isométrica) + vista sorpresa +
  centrar · 10. Reiniciar · 11. Captura PNG del estado actual.
- **Tarjeta de fase actual** en el panel: descripción escolar + tip **"👀 Observa:"**.
- **Leyenda de piezas clicable** (chips con punto de color) + atajos de teclado.
- **Responsive ≤920px:** apilado (escena arriba ~58vh, panel debajo), todo accesible.
- **Scrollbars propias** (thumb degradado azul→naranja, track oscuro, hover) en panel
  y cualquier zona con scroll. Microinteracciones: hover con elevación, toasts,
  entradas escalonadas, `focus-visible`, `prefers-reduced-motion`.

### 3.4 · Funciones 3D obligatorias
- Órbita con arrastre + zoom con rueda (`OrbitControls` con damping), calidad completa
  mientras se arrastra (sin bajar resolución ni apagar efectos al interactuar).
- Iluminación dramática: hemisférica + key cálida con sombras PCFSoft + rim azul +
  fill cálido + luz puntual ligada a eventos; `RoomEnvironment` para reflejos;
  `ACESFilmicToneMapping`; **bloom sutil** (umbral ~0.78) para destellos y emisivos.
- **Etiquetas HTML en el idioma elegido** sobre cada pieza, con línea guía SVG y punto
  de anclaje, offset por pieza, toggle, y clic para seleccionar.
- **Despiece real:** cada pieza tiene posición ensamblada + offset de despiece (+ pose
  estática si es móvil); interpolación suave con `smooth(explode)`; la cámara se
  reencuadra sola al despiezar; botón alterna DESPIECE ↔ ARMAR y pausa/reanuda.
- **Selección de piezas:** raycaster (clic vs arrastre <6px/<450ms), resaltado con
  pulso emisivo, hover sutil, ficha con nombre + función escolar; sincronizada entre
  3D, etiquetas y leyenda; `Esc` o clic vacío deselecciona.
- **Partículas de flujo** del tema (sangre, agua, electrones, humo…) ligadas a las
  fases + polvo ambiental; se atenúan con el despiece.
- **Cinemática correcta y simplificada** del fenómeno (la matemática real del tema:
  órbitas, ciclo cardíaco, leva-válvula, etc.), gobernada por una **variable maestra
  de progreso** (como el ángulo 0–720° del motor) con función central `setProgress()`
  que detecta cruces de umbral y dispara **eventos** (destello + sonido), igual que
  la chispa del motor.
- Tweens de progreso (paso a paso, saltos desde la línea de tiempo) y de cámara;
  calidad por niveles: dpr (2 / 1.5 / 1), bloom on/on/off, sombras 2048/1024/off,
  partículas 120/80/40.

### 3.5 · Mapa de adaptación (motor → tu tema)
| En la muestra (motor)            | En el tema pedido                                   |
|----------------------------------|-----------------------------------------------------|
| Ciclo 0–720°                     | Variable maestra de progreso del fenómeno           |
| 4 tiempos                        | 2–6 fases con color propio (legibles, distinguibles)|
| Chispa / explosión               | Evento(s) clave con destello, luz y sonido          |
| Pistón / biela / cigüeñal        | Componentes móviles con su cinemática real          |
| Despiece vertical                | Separación de componentes o capas del tema          |
| Corte transversal                | Corte con clipping planes, o rayos X/transparencia  |
| Partículas azules / humo         | Flujos del tema (sangre, agua, corriente, gases…)   |
| RPM                              | Velocidad con unidades del tema (BPM, años/s, etc.) |
| PMS / PMI                        | Hitos conceptuales del fenómeno                     |

Si el tema no es un objeto ensamblado (paisaje, proceso), **reinterpretar el despiece
como vista expandida de capas/elementos; nunca omitir el botón.** Si es un fenómeno
silencioso, usar ambience suave ligada a lo visible o respetar `SONIDO: no`.

### 3.6 · Dirección de arte (la huella del estilo)
- Paleta derivada del tema con **7–8 tonos**: familia dominante saturada en las
  superficies grandes + 2–3 acentos de croma pleno + tonos semánticos (éxito, aviso,
  peligro, información) + neutros fríos y cálidos para fondo/superficie/overlay.
  Gradientes entre tonos realmente distintos; bordes, iconos y brillos toman colores
  de la paleta; nada de gris plano por defecto; contraste legible en todo par texto/fondo.
- Materiales `MeshStandardMaterial` con metalness/roughness variados y emisivos para
  eventos; geometría por primitivas y curvas (nada de modelos externos).
- Textos nivel escolar: frases cortas, científicamente exactos, sin jerga innecesaria;
  cada pieza con función en 1–2 frases; cada fase con descripción + "👀 Observa:".
- Sonido **procedural WebAudio** (sin archivos): zumbido base ligado a la velocidad +
  eventos sincronizados con lo visible; `AudioContext` perezoso desbloqueado en el
  primer gesto; volumen bajo; un solo botón arriba silencia todo.

### 3.7 · Arquitectura recomendada (espejo del código de muestra)
- Datos separados: `PHASES[]` (name, color, sub, motion, desc, tip) y `PARTS{}`
  (name, color, desc) + orden de leyenda.
- Registro de piezas: `part(id, base, offset, pose)` → grupo con `userData.partId`;
  ejes giratorios con patrón pivote→rotación; materiales creados con helper `M()`
  que registra en `allMats`/`clipMats` y guarda emisivo base para restaurar.
- Etiquetas: `Object3D` ancla por pieza → proyección NDC por frame → pills HTML +
  líneas SVG; se ocultan si quedan detrás de cámara o fuera de pantalla.
- Estado único sincronizado con todos los controles; toasts para cada acción;
  reiniciar restaura TODO (progreso, velocidad, despiece, toggles, cámara, selección).
- Atajos estándar: `Espacio` play/pausa · `E` despiece · `→` siguiente fase ·
  `C` corte · `L` etiquetas · `R` reiniciar · `Esc` cerrar ficha.
- Captura PNG con `preserveDrawingBuffer:true` + flash + toast; pantalla completa.

### 3.8 · Prohibiciones
No múltiples archivos · no build/servidor · no assets externos fuera de CDN · no
frameworks · no loops/listeners duplicados al reiniciar · no romper con resize ·
no texto en otro idioma si `IDIOMA: español` · no placeholders · no afirmar pruebas
que no se realizaron · no entregar un cascarón: todo control debe hacer algo real.

### 3.9 · Criterios de aceptación (autoverifica antes de entregar)
- Abre y renderiza con loader → escena; error de red muestra fallback utilizable.
- Arrastrar orbita suave; rueda hace zoom; presets y vista sorpresa funcionan.
- El fenómeno anima sus fases; insignia, tarjeta, línea de tiempo y lecturas se
  sincronizan; clic en fase salta a ella; paso a paso avanza exactamente una fase.
- Despiece separa todas las piezas con animación y reencuadre; slider parcial en vivo;
  armar restaura; el fenómeno puede reanudarse.
- Etiquetas visibles en el idioma pedido, clicables, con toggle; selección resalta en
  3D + ficha + leyenda; hover y deselección correctos.
- Corte/rayos X conmuta sin errores; sonido liga a eventos y el botón superior silencia.
- Calidad cambia dpr/bloom/sombras/partículas; captura descarga PNG; reiniciar no
  duplica nada; móvil apila sin solapes ni controles inalcanzables.
- Cero errores de consola; un solo bucle de render; recursos disposed al cambiar calidad.

### 3.10 · Disparador final
Cuando hayas leído todo este documento: **lee la PETICIÓN DEL PROFESOR de la sección 2
y entrega ahora el simulador completo del tema pedido.**

---

## 4 · ✅ PRUEBA RÁPIDA PARA EL PROFESOR (2 minutos con el HTML ya abierto)

1. Arrastra el modelo y haz zoom → debe girar suave y verse con brillos y sombras.
2. Mira la línea de tiempo → las fases avanzan solas con colores y textos correctos.
3. Pulsa **DESPIECE** → las piezas se separan y la cámara se aleja; pulsa **ARMAR**.
4. Toca una pieza en 3D o en la leyenda → se ilumina y aparece su explicación.
5. Pulsa el botón de sonido arriba → silencia todo; vuelve a pulsarlo → regresa.
6. Prueba en el celular o ventana estrecha → escena arriba, controles debajo.
7. Pulsa **Captura PNG** → descarga la imagen del estado actual (sirve para guías).

---

## 5 · 📦 CÓDIGO DE MUESTRA — REFERENCIA CANÓNICA DE ESTILO Y ARQUITECTURA

> IA: este es el simulador original del motor de 4 tiempos. Estúdialo como patrón de
> calidad, estructura, CSS, helpers, despiece, etiquetas, sonido y QA. **No lo copies
> como resultado**: construye el tema de la sección 2 con esta misma factura.

```html
<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="color-scheme" content="dark">
<title>Motor de 4 Tiempos · Simulador 3D Interactivo</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Chakra+Petch:wght@500;600;700&family=Inter:wght@400;600;800&display=swap" rel="stylesheet">
<style>
/* ============ PALETA Y BASE ============ */
:root{
  --bg0:#070d18; --bg1:#0c1526; --surface:#101c31; --surface2:#152540; --line:#24385a;
  --ink:#eaf2ff; --muted:#94a9c9;
  --blue:#38bdf8; --blue2:#4da3ff; --amber:#fbbf24; --fire:#ff6a3d; --fire2:#ff3d2e;
  --teal:#7ee0c3; --green:#4ade80; --purple:#c084fc; --lime:#a3e635;
  --grad-fire:linear-gradient(135deg,#ff8a3d,#ff3d2e);
  --grad-blue:linear-gradient(135deg,#4da3ff,#38bdf8);
  --font-d:'Chakra Petch',system-ui,sans-serif; --font-b:'Inter',system-ui,sans-serif;
}
*{margin:0;padding:0;box-sizing:border-box}
html,body{height:100%}
body{
  font-family:var(--font-b); background:var(--bg0); color:var(--ink);
  overflow:hidden; font-size:14px; -webkit-font-smoothing:antialiased;
}
button{font-family:inherit;color:inherit}
::-webkit-scrollbar{width:10px;height:10px}
::-webkit-scrollbar-track{background:var(--bg1)}
::-webkit-scrollbar-thumb{background:linear-gradient(180deg,#3b82f6,#ff7a3d);border-radius:8px;border:2px solid var(--bg1)}
::-webkit-scrollbar-thumb:hover{background:linear-gradient(180deg,#60a5fa,#ffa06a)}
*{scrollbar-width:thin;scrollbar-color:#3b82f6 var(--bg1)}

#app{display:grid;grid-template-columns:1fr 336px;grid-template-rows:60px 1fr;height:100vh;height:100dvh}

/* ============ CABECERA ============ */
header{
  grid-column:1/-1;display:flex;align-items:center;gap:14px;padding:0 18px;
  background:linear-gradient(90deg,#0d1830,#0b1426 55%,#160f14);
  border-bottom:1px solid var(--line);position:relative;z-index:30;
  animation:dropIn .6s cubic-bezier(.2,.9,.3,1) both;
}
header::after{content:"";position:absolute;left:0;right:0;bottom:-1px;height:2px;
  background:linear-gradient(90deg,var(--blue2),var(--purple) 35%,var(--fire) 75%,var(--amber));opacity:.85}
.brand{display:flex;align-items:center;gap:12px;min-width:0}
.brand svg{flex:none}
.brand .piston-anim{animation:pistonBob 1.1s ease-in-out infinite}
@keyframes pistonBob{0%,100%{transform:translateY(0)}50%{transform:translateY(4px)}}
.brand h1{font-family:var(--font-d);font-size:19px;font-weight:700;letter-spacing:.5px;white-space:nowrap}
.brand h1 em{font-style:normal;color:var(--fire)}
.brand p{font-size:11px;color:var(--muted);white-space:nowrap}
.cycle-chip{font-family:var(--font-d);font-size:11px;color:var(--blue);border:1px solid #2a4a7a;
  background:#0e1e38;padding:4px 10px;border-radius:99px;white-space:nowrap}
header .spacer{flex:1}
.hbtn{display:flex;align-items:center;gap:7px;background:var(--surface2);border:1px solid var(--line);
  border-radius:10px;padding:8px 12px;font-size:12.5px;font-weight:600;cursor:pointer;transition:.18s}
.hbtn:hover{border-color:var(--blue2);transform:translateY(-1px);box-shadow:0 4px 16px #4da3ff33}
.hbtn.off{color:var(--muted)}
.hbtn.off .on-ic{display:none}.hbtn:not(.off) .off-ic{display:none}
.hbtn svg{width:16px;height:16px}

/* ============ ESCENARIO 3D ============ */
#stage{position:relative;overflow:hidden;background:var(--bg0)}
#viewport{position:absolute;inset:0}
#viewport canvas{display:block;width:100%;height:100%}
#grain{position:absolute;inset:0;pointer-events:none;opacity:.05;z-index:3;
  background-image:url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="160" height="160"><filter id="n"><feTurbulence type="fractalNoise" baseFrequency="0.9" numOctaves="2"/></filter><rect width="160" height="160" filter="url(%23n)" opacity="0.6"/></svg>')}
#vignette{position:absolute;inset:0;pointer-events:none;z-index:3;
  background:radial-gradient(ellipse at 50% 42%,transparent 52%,rgba(4,8,16,.55) 100%)}

/* Etiquetas de piezas */
#labelsLayer{position:absolute;inset:0;z-index:5;pointer-events:none}
#leaderSvg{position:absolute;inset:0;width:100%;height:100%}
.pill{position:absolute;left:0;top:0;pointer-events:auto;cursor:pointer;
  font-family:var(--font-d);font-size:11.5px;font-weight:600;letter-spacing:.3px;white-space:nowrap;
  background:rgba(9,15,28,.88);border:1px solid var(--pc,#3b82f6);color:var(--ink);
  padding:3px 9px 3px 7px;border-radius:99px;display:flex;align-items:center;gap:6px;
  box-shadow:0 2px 10px rgba(0,0,0,.5);transition:box-shadow .2s,background .2s;backdrop-filter:blur(4px)}
.pill i{width:7px;height:7px;border-radius:50%;background:var(--pc);box-shadow:0 0 6px var(--pc);flex:none}
.pill:hover,.pill.active{background:#13233f;box-shadow:0 0 0 2px var(--pc),0 0 18px var(--pc)}
.pill.active{font-weight:700}

/* Insignia del tiempo actual */
#strokeBadge{position:absolute;top:14px;left:14px;z-index:6;display:flex;align-items:center;gap:12px;
  background:rgba(9,15,28,.82);border:1px solid var(--line);border-left:4px solid var(--sc,var(--blue));
  border-radius:14px;padding:10px 16px 10px 12px;backdrop-filter:blur(8px);
  box-shadow:0 6px 24px rgba(0,0,0,.45),0 0 24px color-mix(in srgb,var(--sc,var(--blue)) 22%,transparent);
  animation:fadeUp .7s .3s cubic-bezier(.2,.9,.3,1) both}
#strokeBadge .num{font-family:var(--font-d);font-size:26px;font-weight:700;width:44px;height:44px;flex:none;
  display:grid;place-items:center;border-radius:12px;background:var(--sc,var(--blue));color:#08101f}
#strokeBadge .name{font-family:var(--font-d);font-size:18px;font-weight:700;letter-spacing:1px;color:var(--sc,var(--blue))}
#strokeBadge .sub{font-size:10.5px;color:var(--muted)}
#strokeBadge .dead{font-family:var(--font-d);font-size:10px;font-weight:700;color:#08101f;background:var(--amber);
  padding:2px 7px;border-radius:6px;margin-left:6px;visibility:hidden}
#strokeBadge.pop{animation:pop .45s cubic-bezier(.2,.9,.3,1)}
@keyframes pop{0%{transform:scale(1.07)}100%{transform:scale(1)}}

#hintChip{position:absolute;top:14px;right:14px;z-index:6;font-size:11.5px;color:var(--muted);
  background:rgba(9,15,28,.75);border:1px solid var(--line);border-radius:99px;padding:7px 13px;
  backdrop-filter:blur(6px);transition:opacity 1s;animation:fadeUp .7s .5s both}
#hintChip b{color:var(--ink)}

/* Ficha de pieza */
#infoCard{position:absolute;left:14px;bottom:122px;z-index:7;width:min(340px,calc(100% - 28px));
  background:rgba(10,17,31,.92);border:1px solid var(--ic,#3b82f6);border-radius:14px;padding:14px 16px;
  backdrop-filter:blur(10px);box-shadow:0 10px 34px rgba(0,0,0,.55),0 0 22px color-mix(in srgb,var(--ic,#3b82f6) 20%,transparent);
  transform:translateY(12px);opacity:0;pointer-events:none;transition:.28s cubic-bezier(.2,.9,.3,1)}
#infoCard.show{transform:translateY(0);opacity:1;pointer-events:auto}
#infoCard .eyebrow{font-size:9.5px;letter-spacing:2px;color:var(--ic,#3b82f6);font-weight:800;text-transform:uppercase}
#infoCard h4{font-family:var(--font-d);font-size:17px;margin:3px 0 6px;display:flex;align-items:center;gap:8px}
#infoCard h4 i{width:10px;height:10px;border-radius:50%;background:var(--ic);box-shadow:0 0 8px var(--ic)}
#infoCard p{font-size:12.5px;line-height:1.55;color:#c6d4ea}
#infoCard .close{position:absolute;top:8px;right:10px;background:none;border:none;color:var(--muted);
  font-size:18px;cursor:pointer;line-height:1;padding:4px}
#infoCard .close:hover{color:var(--ink)}

/* Línea de tiempo del ciclo */
#timeline{position:absolute;left:12px;right:12px;bottom:12px;z-index:6;
  background:rgba(9,14,26,.82);border:1px solid var(--line);border-radius:14px;padding:10px 14px 8px;
  backdrop-filter:blur(10px);box-shadow:0 8px 30px rgba(0,0,0,.5);animation:fadeUp .7s .45s both}
.tl-segs{display:flex;gap:4px;position:relative}
.tl-seg{flex:1;background:none;border:none;cursor:pointer;text-align:left;padding:0 2px;min-width:0}
.tl-seg .tl-name{font-family:var(--font-d);font-size:11.5px;font-weight:600;color:var(--muted);
  display:flex;align-items:center;gap:6px;margin-bottom:5px;white-space:nowrap;transition:.2s}
.tl-seg .tl-name i{font-style:normal;width:16px;height:16px;flex:none;display:grid;place-items:center;
  border-radius:5px;background:#1b2c49;color:var(--muted);font-size:10px;transition:.2s}
.tl-seg .tl-bar{display:block;height:9px;border-radius:6px;background:#152340;overflow:hidden;border:1px solid #1e3153}
.tl-seg .tl-fill{display:block;height:100%;background:var(--sc);transform-origin:left;transform:scaleX(0);border-radius:6px}
.tl-seg.done .tl-fill{transform:scaleX(1);opacity:.35}
.tl-seg.done .tl-name{color:#b9c8e2}
.tl-seg.active .tl-name{color:var(--sc);text-shadow:0 0 12px var(--sc)}
.tl-seg.active .tl-name i{background:var(--sc);color:#08101f}
.tl-seg.active .tl-bar{box-shadow:0 0 12px color-mix(in srgb,var(--sc) 55%,transparent)}
.tl-seg:hover .tl-name{color:var(--ink)}
#tlMarker{position:absolute;top:16px;bottom:-2px;width:2px;background:#fff;border-radius:2px;
  box-shadow:0 0 8px #fff;pointer-events:none;left:0}
#tlMarker::before{content:"";position:absolute;top:-5px;left:-3px;border:4px solid transparent;border-top-color:#fff}
.tl-ticks{position:relative;height:12px;margin-top:3px;font-family:var(--font-d);font-size:8.5px;color:#5f7398}
.tl-ticks span{position:absolute;transform:translateX(-50%)}
.tl-read{display:flex;justify-content:space-between;gap:10px;font-family:var(--font-d);font-size:11px;
  color:var(--muted);margin-top:2px;font-variant-numeric:tabular-nums;flex-wrap:wrap}
.tl-read b{color:var(--ink)}

/* Cargador / error */
#loader{position:absolute;inset:0;z-index:20;display:grid;place-items:center;
  background:radial-gradient(ellipse at 30% 20%,#12233f,#070d18 70%);transition:opacity .6s}
#loader.done{opacity:0;pointer-events:none}
.load-box{text-align:center}
.load-box svg{margin-bottom:14px}
.load-box .lp{animation:pistonBob .8s ease-in-out infinite}
.load-box h2{font-family:var(--font-d);font-size:18px;letter-spacing:1px}
.load-box p{color:var(--muted);font-size:12px;margin-top:6px;max-width:320px;line-height:1.5}
.load-bar{width:180px;height:4px;background:#152340;border-radius:4px;margin:16px auto 0;overflow:hidden}
.load-bar i{display:block;height:100%;width:40%;border-radius:4px;background:var(--grad-blue);animation:slide 1.1s ease-in-out infinite}
@keyframes slide{0%{transform:translateX(-100%)}100%{transform:translateX(280%)}}
.load-box .btn{margin-top:16px}

#flash{position:absolute;inset:0;background:#fff;opacity:0;pointer-events:none;z-index:15;transition:opacity .18s}
#flash.on{opacity:.7}

/* ============ PANEL DE CONTROL ============ */
#panel{background:linear-gradient(180deg,#0d1729,#0a1220);border-left:1px solid var(--line);
  overflow-y:auto;overflow-x:hidden;padding:16px 16px 22px;z-index:10;animation:slideIn .6s .15s cubic-bezier(.2,.9,.3,1) both}
.sec{margin-bottom:20px}
.sec-title{font-family:var(--font-d);font-size:11px;font-weight:700;letter-spacing:2.5px;text-transform:uppercase;
  color:var(--muted);display:flex;align-items:center;gap:8px;margin-bottom:11px}
.sec-title::before{content:"";width:14px;height:3px;border-radius:2px;background:var(--grad-fire)}
.sec-title.blue::before{background:var(--grad-blue)}

.btn{display:inline-flex;align-items:center;justify-content:center;gap:8px;background:var(--surface2);
  border:1px solid var(--line);border-radius:11px;padding:10px 12px;font-size:12.5px;font-weight:600;
  cursor:pointer;transition:.18s;user-select:none}
.btn:hover{border-color:var(--blue2);transform:translateY(-1px);box-shadow:0 5px 18px #4da3ff2e}
.btn:active{transform:translateY(0) scale(.98)}
.btn svg{width:15px;height:15px;flex:none}
.btn-primary{background:linear-gradient(135deg,#1c3f6e,#173257);border-color:#2f5b96}
.btn-primary:hover{border-color:var(--blue);box-shadow:0 5px 20px #38bdf84d}
.btn-fire{background:var(--grad-fire);border-color:#ff9a5c;color:#fff;font-family:var(--font-d);
  font-size:14px;font-weight:700;letter-spacing:.6px;padding:13px 12px;text-shadow:0 1px 2px rgba(0,0,0,.3)}
.btn-fire:hover{box-shadow:0 6px 24px #ff5c3d66;border-color:#ffc09a}
.btn-fire.armed{background:linear-gradient(135deg,#1f4d40,#173a30);border-color:#3e8f6e}
.wide{width:100%}
.row2{display:grid;grid-template-columns:1fr 1fr;gap:8px}
.rowcam{display:grid;grid-template-columns:1fr 1fr;gap:8px}

.ctl-row{margin-top:12px}
.ctl-lab{display:flex;justify-content:space-between;align-items:baseline;font-size:12px;font-weight:600;margin-bottom:7px}
.ctl-lab output{font-family:var(--font-d);color:var(--blue);font-size:12.5px;font-variant-numeric:tabular-nums}
.ctl-lab output.fire{color:var(--fire)}
.ctl-hint{font-size:10.5px;color:#64789c;margin-top:5px;line-height:1.4}
input[type=range]{-webkit-appearance:none;appearance:none;width:100%;height:6px;border-radius:6px;outline:none;cursor:pointer;
  background:linear-gradient(90deg,var(--rc,#38bdf8) var(--p,50%),#152340 var(--p,50%))}
input[type=range]::-webkit-slider-thumb{-webkit-appearance:none;width:18px;height:18px;border-radius:50%;
  background:#fff;border:3px solid var(--rc,#38bdf8);box-shadow:0 0 10px var(--rc,#38bdf8);cursor:grab;transition:.15s}
input[type=range]::-webkit-slider-thumb:hover{transform:scale(1.15)}
input[type=range]::-moz-range-thumb{width:14px;height:14px;border-radius:50%;background:#fff;border:3px solid var(--rc,#38bdf8);box-shadow:0 0 10px var(--rc,#38bdf8);cursor:grab}
input[type=range]:focus-visible{box-shadow:0 0 0 3px #4da3ff55}

.switch-row{display:flex;justify-content:space-between;align-items:center;padding:8px 2px;font-size:12.5px;font-weight:600;cursor:pointer}
.switch-row small{display:block;font-weight:400;font-size:10.5px;color:#64789c}
.switch{position:relative;width:42px;height:23px;flex:none}
.switch input{position:absolute;opacity:0;inset:0;cursor:pointer;z-index:2}
.switch i{position:absolute;inset:0;border-radius:99px;background:#1a2b49;border:1px solid var(--line);transition:.2s}
.switch i::after{content:"";position:absolute;top:2px;left:2px;width:17px;height:17px;border-radius:50%;
  background:#8195b5;transition:.2s cubic-bezier(.2,.9,.3,1)}
.switch input:checked + i{background:color-mix(in srgb,var(--sw,#38bdf8) 30%,#12233f);border-color:var(--sw,#38bdf8)}
.switch input:checked + i::after{left:21px;background:var(--sw,#38bdf8);box-shadow:0 0 10px var(--sw,#38bdf8)}
.switch input:focus-visible + i{box-shadow:0 0 0 3px #4da3ff55}

select{width:100%;background:var(--surface2);border:1px solid var(--line);color:var(--ink);border-radius:10px;
  padding:9px 10px;font-size:12.5px;font-family:inherit;cursor:pointer;outline:none}
select:hover{border-color:var(--blue2)}

/* Tarjeta del tiempo actual */
#strokeCard{background:linear-gradient(160deg,color-mix(in srgb,var(--sc,#38bdf8) 13%,#0f1c33),#0d1729);
  border:1px solid color-mix(in srgb,var(--sc,#38bdf8) 45%,#24385a);border-radius:14px;padding:13px 14px;transition:.3s}
#strokeCard .sc-head{display:flex;align-items:center;gap:10px;margin-bottom:7px}
#strokeCard .sc-num{font-family:var(--font-d);font-size:20px;font-weight:700;width:34px;height:34px;flex:none;
  display:grid;place-items:center;border-radius:9px;background:var(--sc,#38bdf8);color:#08101f}
#strokeCard h4{font-family:var(--font-d);font-size:16px;letter-spacing:.5px;color:var(--sc,#38bdf8)}
#strokeCard .sc-sub{font-size:10px;color:var(--muted)}
#strokeCard p{font-size:12.5px;line-height:1.55;color:#cfdbef}
#strokeCard .sc-tip{margin-top:9px;font-size:11px;line-height:1.45;color:var(--sc,#38bdf8);
  background:rgba(8,14,26,.55);border-radius:9px;padding:7px 9px;border:1px dashed color-mix(in srgb,var(--sc,#38bdf8) 40%,transparent)}

/* Leyenda de piezas */
#legend{display:grid;grid-template-columns:1fr 1fr;gap:6px}
.chip{display:flex;align-items:center;gap:7px;background:var(--surface);border:1px solid var(--line);
  border-radius:9px;padding:7px 8px;font-size:11px;font-weight:600;cursor:pointer;transition:.15s;text-align:left;min-width:0}
.chip span{overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.chip i{width:8px;height:8px;flex:none;border-radius:50%;background:var(--pc);box-shadow:0 0 6px var(--pc)}
.chip:hover{border-color:var(--pc);transform:translateY(-1px)}
.chip.active{border-color:var(--pc);background:#152743;box-shadow:0 0 12px color-mix(in srgb,var(--pc) 35%,transparent)}

.keys{font-size:10.5px;color:#5f7398;line-height:1.7;margin-top:12px}
.keys b{color:var(--muted);font-family:var(--font-d);background:#152340;border:1px solid var(--line);
  border-radius:5px;padding:1px 5px;font-size:9.5px}

/* Avisos */
#toasts{position:fixed;bottom:18px;left:50%;transform:translateX(-50%);z-index:60;display:flex;flex-direction:column;gap:8px;align-items:center;pointer-events:none}
.toast{font-family:var(--font-d);font-size:12.5px;font-weight:600;background:rgba(13,23,41,.95);
  border:1px solid var(--blue2);border-radius:99px;padding:9px 18px;box-shadow:0 8px 26px rgba(0,0,0,.5),0 0 16px #4da3ff33;
  animation:toastIn .3s cubic-bezier(.2,.9,.3,1),toastOut .3s 2.1s both}
@keyframes toastIn{from{transform:translateY(14px);opacity:0}}
@keyframes toastOut{to{transform:translateY(8px);opacity:0}}

@keyframes fadeUp{from{transform:translateY(14px);opacity:0}to{transform:translateY(0);opacity:1}}
@keyframes dropIn{from{transform:translateY(-100%)}to{transform:translateY(0)}}
@keyframes slideIn{from{transform:translateX(40px);opacity:0}to{transform:translateX(0);opacity:1}}

/* ============ RESPONSIVE ============ */
@media (max-width:920px){
  body{overflow:auto}
  #app{grid-template-columns:1fr;grid-template-rows:56px 58vh auto;height:auto}
  #stage{min-height:420px}
  #panel{border-left:none;border-top:1px solid var(--line);max-height:none}
  .brand p,.cycle-chip{display:none}
  .brand h1{font-size:16px}
  #strokeBadge{padding:7px 11px 7px 9px;gap:9px}
  #strokeBadge .num{width:34px;height:34px;font-size:19px}
  #strokeBadge .name{font-size:14px}
  #hintChip{display:none}
  .pill{font-size:10px;padding:2px 7px 2px 6px}
  .tl-seg .tl-name{font-size:9.5px;gap:4px}
  .tl-seg .tl-name i{width:13px;height:13px;font-size:8.5px}
  .tl-read{font-size:9.5px}
  #infoCard{bottom:108px}
  #timeline{padding:8px 10px 6px}
}
@media (prefers-reduced-motion:reduce){
  *{animation-duration:.01s !important}
}
</style>
<script type="importmap">
{ "imports": {
  "three": "https://cdn.jsdelivr.net/npm/three@0.160.0/build/three.module.js",
  "three/addons/": "https://cdn.jsdelivr.net/npm/three@0.160.0/examples/jsm/"
} }
</script>
</head>
<body>
<div id="app">

  <!-- ================= CABECERA ================= -->
  <header>
    <div class="brand">
      <svg width="34" height="34" viewBox="0 0 34 34" fill="none" aria-hidden="true">
        <rect x="8" y="3" width="18" height="24" rx="3" stroke="#4da3ff" stroke-width="2"/>
        <g class="piston-anim">
          <rect x="11" y="7" width="12" height="7" rx="1.5" fill="#ff6a3d"/>
          <line x1="17" y1="14" x2="17" y2="21" stroke="#eaf2ff" stroke-width="2.4" stroke-linecap="round"/>
        </g>
        <circle cx="17" cy="24" r="3.4" stroke="#fbbf24" stroke-width="2"/>
      </svg>
      <div>
        <h1>MOTOR <em>4 TIEMPOS</em></h1>
        <p>Simulador educativo 3D · Motor de gasolina</p>
      </div>
    </div>
    <span class="cycle-chip">4 tiempos = 720° = 2 vueltas del cigüeñal</span>
    <div class="spacer"></div>
    <button class="hbtn" id="soundBtn" aria-label="Activar o silenciar sonido" aria-pressed="true">
      <svg class="on-ic" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"><path d="M11 5 6 9H2v6h4l5 4z" fill="currentColor" stroke="none"/><path d="M15.5 8.5a5 5 0 0 1 0 7"/><path d="M18.5 5.5a9 9 0 0 1 0 13"/></svg>
      <svg class="off-ic" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"><path d="M11 5 6 9H2v6h4l5 4z" fill="currentColor" stroke="none"/><line x1="16" y1="9" x2="22" y2="15"/><line x1="22" y1="9" x2="16" y2="15"/></svg>
      <span id="soundLabel">Sonido</span>
    </button>
    <button class="hbtn" id="fsBtn" aria-label="Pantalla completa">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"><path d="M8 3H5a2 2 0 0 0-2 2v3M16 3h3a2 2 0 0 1 2 2v3M8 21H5a2 2 0 0 1-2-2v-3M16 21h3a2 2 0 0 0 2-2v-3"/></svg>
    </button>
  </header>

  <!-- ================= ESCENA ================= -->
  <main id="stage">
    <div id="viewport"></div>
    <div id="grain"></div><div id="vignette"></div>
    <div id="labelsLayer"><svg id="leaderSvg"></svg></div>

    <div id="strokeBadge">
      <div class="num" id="badgeNum">1</div>
      <div>
        <div class="name" id="badgeName">ADMISIÓN<span class="dead" id="deadChip">PMS</span></div>
        <div class="sub" id="badgeSub">Tiempo 1 de 4 · el pistón baja</div>
      </div>
    </div>

    <div id="hintChip">🖱️ <b>Arrastra</b> para girar · <b>Rueda</b> para zoom · <b>Toca una pieza</b> para saber qué hace</div>

    <div id="infoCard" role="dialog" aria-label="Información de la pieza">
      <button class="close" id="infoClose" aria-label="Cerrar">×</button>
      <div class="eyebrow">Pieza del motor</div>
      <h4><i></i><span id="infoName"></span></h4>
      <p id="infoDesc"></p>
    </div>

    <div id="timeline">
      <div class="tl-segs" id="tlSegs">
        <button class="tl-seg" data-i="0" style="--sc:#38bdf8"><span class="tl-name"><i>1</i>Admisión</span><span class="tl-bar"><span class="tl-fill"></span></span></button>
        <button class="tl-seg" data-i="1" style="--sc:#fbbf24"><span class="tl-name"><i>2</i>Compresión</span><span class="tl-bar"><span class="tl-fill"></span></span></button>
        <button class="tl-seg" data-i="2" style="--sc:#ff5c3d"><span class="tl-name"><i>3</i>Explosión</span><span class="tl-bar"><span class="tl-fill"></span></span></button>
        <button class="tl-seg" data-i="3" style="--sc:#7ee0c3"><span class="tl-name"><i>4</i>Escape</span><span class="tl-bar"><span class="tl-fill"></span></span></button>
        <div id="tlMarker"></div>
      </div>
      <div class="tl-ticks">
        <span style="left:0%">PMS</span><span style="left:25%">PMI</span><span style="left:50%">PMS</span><span style="left:75%">PMI</span><span style="left:100%">PMS</span>
      </div>
      <div class="tl-read">
        <span>Cigüeñal: <b id="angleTxt">0°</b> / 720° · Vuelta <b id="lapTxt">1</b> de 2</span>
        <span><b id="rpmTxt">50 RPM</b> · Ciclos: <b id="cyclesTxt">0</b> · PMS/PMI = punto muerto sup./inf.</span>
      </div>
    </div>

    <div id="flash"></div>
    <div id="loader">
      <div class="load-box" id="loadBox">
        <svg width="64" height="64" viewBox="0 0 34 34" fill="none">
          <rect x="8" y="3" width="18" height="24" rx="3" stroke="#4da3ff" stroke-width="2"/>
          <g class="lp"><rect x="11" y="7" width="12" height="7" rx="1.5" fill="#ff6a3d"/>
          <line x1="17" y1="14" x2="17" y2="21" stroke="#eaf2ff" stroke-width="2.4" stroke-linecap="round"/></g>
          <circle cx="17" cy="24" r="3.4" stroke="#fbbf24" stroke-width="2"/>
        </svg>
        <h2>PREPARANDO EL MOTOR…</h2>
        <p>Cargando el laboratorio 3D del motor de gasolina.</p>
        <div class="load-bar"><i></i></div>
      </div>
    </div>
  </main>

  <!-- ================= PANEL ================= -->
  <aside id="panel">
    <div class="sec">
      <h3 class="sec-title">Controles del motor</h3>
      <div class="row2">
        <button class="btn btn-primary" id="playBtn">
          <svg id="icPause" viewBox="0 0 24 24" fill="currentColor"><rect x="6" y="4" width="4" height="16" rx="1"/><rect x="14" y="4" width="4" height="16" rx="1"/></svg>
          <svg id="icPlay" viewBox="0 0 24 24" fill="currentColor" style="display:none"><path d="M7 4.5v15l13-7.5z"/></svg>
          <span id="playLabel">Pausar</span>
        </button>
        <button class="btn" id="stepBtn" title="Avanza exactamente un tiempo (180°)">
          <svg viewBox="0 0 24 24" fill="currentColor"><path d="M5 4.5v15l10-7.5z"/><rect x="17" y="4" width="3" height="16" rx="1"/></svg>
          Siguiente tiempo
        </button>
      </div>
      <div class="ctl-row">
        <div class="ctl-lab"><span>Velocidad del motor</span><output id="rpmOut">50 RPM</output></div>
        <input type="range" id="rpmSlider" min="6" max="240" step="2" value="50" style="--rc:#38bdf8" aria-label="Velocidad en RPM">
        <div class="ctl-hint">Gira lento a propósito (cámara lenta educativa) para observar cada tiempo.</div>
      </div>
      <div class="ctl-row">
        <button class="btn btn-fire wide" id="explodeBtn" aria-pressed="false">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round"><path d="M12 9V3m0 0-3 3m3-3 3 3M12 15v6m0 0-3-3m3 3 3-3M9 12H3m0 0 3-3m-3 3 3 3M15 12h6m0 0-3-3m3 3-3 3"/></svg>
          <span id="explodeLabel">DESPIECE DEL MOTOR</span>
        </button>
      </div>
      <div class="ctl-row">
        <div class="ctl-lab"><span>Separación de piezas</span><output class="fire" id="sepOut">0%</output></div>
        <input type="range" id="sepSlider" min="0" max="100" step="1" value="0" style="--rc:#ff6a3d" aria-label="Separación del despiece">
      </div>
    </div>

    <div class="sec">
      <h3 class="sec-title blue">Tiempo actual</h3>
      <div id="strokeCard">
        <div class="sc-head">
          <div class="sc-num" id="scNum">1</div>
          <div><h4 id="scName" aria-live="polite">Admisión</h4><div class="sc-sub" id="scSub">0° – 180° · 1ª vuelta</div></div>
        </div>
        <p id="scDesc"></p>
        <div class="sc-tip" id="scTip"></div>
      </div>
    </div>

    <div class="sec">
      <h3 class="sec-title blue">Visualización</h3>
      <label class="switch-row"><span>Corte transversal<small>Abre el motor para ver el interior</small></span>
        <span class="switch" style="--sw:#38bdf8"><input type="checkbox" id="cutToggle" checked><i></i></span></label>
      <label class="switch-row"><span>Etiquetas de piezas<small>Nombres en español sobre el modelo</small></span>
        <span class="switch" style="--sw:#a3e635"><input type="checkbox" id="labelsToggle" checked><i></i></span></label>
      <label class="switch-row"><span>Giro automático<small>La cámara orbita sola</small></span>
        <span class="switch" style="--sw:#c084fc"><input type="checkbox" id="rotToggle"><i></i></span></label>
      <div class="ctl-row">
        <div class="ctl-lab"><span>Calidad gráfica</span></div>
        <select id="qualitySel" aria-label="Calidad gráfica">
          <option value="alta">Alta (brillos y sombras)</option>
          <option value="media" selected>Media (recomendada)</option>
          <option value="baja">Baja (equipos lentos)</option>
        </select>
      </div>
    </div>

    <div class="sec">
      <h3 class="sec-title blue">Cámara</h3>
      <div class="rowcam">
        <button class="btn cam-btn" data-view="front">Frontal (corte)</button>
        <button class="btn cam-btn" data-view="side">Lateral</button>
        <button class="btn cam-btn" data-view="top">Superior</button>
        <button class="btn cam-btn" data-view="iso">Isométrica</button>
      </div>
      <div class="row2" style="margin-top:8px">
        <button class="btn" id="randomBtn">🎲 Vista sorpresa</button>
        <button class="btn" id="centerBtn">⟳ Centrar</button>
      </div>
    </div>

    <div class="sec">
      <h3 class="sec-title">Piezas del motor</h3>
      <div id="legend"></div>
      <div class="ctl-hint" style="margin-top:8px">Toca una pieza (aquí o en el modelo 3D) para leer su función.</div>
    </div>

    <div class="sec">
      <h3 class="sec-title">Acciones</h3>
      <div class="row2">
        <button class="btn" id="resetBtn">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"><path d="M3 12a9 9 0 1 0 3-6.7L3 8"/><path d="M3 3v5h5"/></svg>
          Reiniciar
        </button>
        <button class="btn btn-primary" id="shotBtn">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"><path d="M4 7h3l2-2h6l2 2h3a1 1 0 0 1 1 1v11a1 1 0 0 1-1 1H4a1 1 0 0 1-1-1V8a1 1 0 0 1 1-1z"/><circle cx="12" cy="13" r="4"/></svg>
          Captura PNG
        </button>
      </div>
      <div class="keys">
        Atajos: <b>Espacio</b> reproducir/pausar · <b>E</b> despiece · <b>→</b> siguiente tiempo ·
        <b>C</b> corte · <b>L</b> etiquetas · <b>R</b> reiniciar
      </div>
    </div>
  </aside>
</div>
<div id="toasts"></div>

<script type="module">
/* ============================================================
   SIMULADOR 3D · MOTOR DE GASOLINA DE 4 TIEMPOS
   ============================================================ */
const $ = s => document.querySelector(s);
const RAD = Math.PI/180;
const clamp=(v,a,b)=>Math.max(a,Math.min(b,v));
const lerp=(a,b,t)=>a+(b-a)*t;
const easeIO=t=>t<.5?4*t*t*t:1-Math.pow(-2*t+2,3)/2;
const smooth=t=>t*t*(3-2*t);

/* ---------- Datos educativos (en español) ---------- */
const STROKES=[
 {name:'Admisión',color:'#38bdf8',sub:'0° – 180° · 1ª vuelta',motion:'el pistón baja',
  desc:'La válvula de admisión se abre y el pistón baja, aspirando la mezcla de aire y gasolina hacia dentro del cilindro.',
  tip:'👀 Observa: la válvula de admisión está abierta y las partículas azules entran al cilindro.'},
 {name:'Compresión',color:'#fbbf24',sub:'180° – 360° · 1ª vuelta',motion:'el pistón sube',
  desc:'Las dos válvulas se cierran y el pistón sube comprimiendo la mezcla. Cuanto más comprimida, más fuerte será la explosión.',
  tip:'👀 Observa: ambas válvulas cerradas; el gas azul se vuelve ámbar al comprimirse.'},
 {name:'Explosión',color:'#ff5c3d',sub:'360° – 540° · 2ª vuelta',motion:'el pistón baja con fuerza',
  desc:'La bujía produce una chispa ⚡ y la mezcla explota. Los gases en expansión empujan el pistón hacia abajo: es el único tiempo que produce trabajo (también llamado carrera de expansión).',
  tip:'👀 Observa: el destello de la bujía al inicio y el brillo naranja que empuja el pistón.'},
 {name:'Escape',color:'#7ee0c3',sub:'540° – 720° · 2ª vuelta',motion:'el pistón sube',
  desc:'La válvula de escape se abre y el pistón sube expulsando los gases quemados hacia el tubo de escape. ¡Y el ciclo vuelve a empezar!',
  tip:'👀 Observa: la válvula de escape abierta y el humo gris saliendo por el conducto naranja.'}
];
const PARTS={
 bujia:{name:'Bujía',color:'#ffd166',desc:'Crea una chispa eléctrica en el momento exacto para inflamar la mezcla de aire y gasolina comprimida, justo antes de la explosión.'},
 valvula_admision:{name:'Válvula de admisión',color:'#38bdf8',desc:'Compuerta que se abre durante la admisión para dejar entrar la mezcla de aire y gasolina al cilindro. La abre el árbol de levas.'},
 valvula_escape:{name:'Válvula de escape',color:'#ff8a5c',desc:'Compuerta que se abre durante el escape para dejar salir los gases ya quemados hacia el tubo de escape.'},
 arbol_levas:{name:'Árbol de levas',color:'#c084fc',desc:'Eje con levas (bultos con forma de huevo) que empuja las válvulas para abrirlas en el momento justo. Gira a la mitad de la velocidad del cigüeñal.'},
 piston:{name:'Pistón',color:'#e2e8f0',desc:'Sube y baja dentro del cilindro. Recibe el empuje de la explosión y lo transmite a la biela. Los segmentos (aros) sellan el espacio para que no se escapen los gases.'},
 biela:{name:'Biela',color:'#cbd5e1',desc:'Une el pistón con el cigüeñal. Junto con el cigüeñal convierte el movimiento rectilíneo (sube y baja) en movimiento giratorio.'},
 ciguenal:{name:'Cigüeñal',color:'#94a3b8',desc:'Eje acodado que gira con los empujes del pistón. Es la salida de potencia del motor: de aquí sale el movimiento hacia las ruedas. Da 2 vueltas por cada ciclo completo.'},
 volante:{name:'Volante de inercia',color:'#f4a261',desc:'Disco pesado que gira con el cigüeñal. Su inercia mantiene el giro suave y ayuda a completar los tiempos que no producen fuerza.'},
 cilindro:{name:'Cilindro',color:'#9bb8d4',desc:'Pared cilíndrica («camisa») que guía al pistón. Dentro ocurre todo: admisión, compresión, explosión y escape. Las aletas ayudan a refrigerar.'},
 culata:{name:'Culata',color:'#b7c6da',desc:'Tapa superior del cilindro. Aloja las válvulas, la bujía y los conductos de entrada y salida de gases. Aquí está la cámara de combustión.'},
 carter:{name:'Cárter',color:'#8b9bb4',desc:'Caja inferior que protege al cigüeñal y almacena el aceite que lubrica todo el motor (se ve en ámbar en el fondo).'},
 conducto_admision:{name:'Conducto de admisión',color:'#4cc9f0',desc:'Tubo por donde entra la mezcla de aire y gasolina (partículas azules) hacia el cilindro cuando abre la válvula de admisión.'},
 conducto_escape:{name:'Conducto de escape',color:'#e07a5f',desc:'Tubo por donde salen los gases quemados (humo gris) después de la explosión. Por eso se calienta tanto.'},
 correa:{name:'Correa de distribución',color:'#a3e635',desc:'Correa dentada que sincroniza el cigüeñal con los árboles de levas: gracias a ella las válvulas se abren justo a tiempo, 1 vez por cada 2 vueltas del cigüeñal.'}
};
const LEGEND_ORDER=['bujia','valvula_admision','valvula_escape','arbol_levas','piston','biela','ciguenal','volante','cilindro','culata','carter','conducto_admision','conducto_escape','correa'];

/* ---------- Estado global ---------- */
const state={
 angle:0, rpm:50, playing:true, cycles:0,
 explode:0, explodeTarget:0, wasPlaying:true,
 cutaway:true, labels:true, autoRot:false, sound:true, quality:'media',
 selected:null, hovered:null, stepMode:false
};

/* ---------- Avisos ---------- */
function toast(msg){
 const t=document.createElement('div'); t.className='toast'; t.textContent=msg;
 $('#toasts').appendChild(t); setTimeout(()=>t.remove(),2500);
}
function fatal(msg){
 $('#loadBox').innerHTML=`<div style="font-size:40px">⚠️</div><h2>NO SE PUDO INICIAR</h2>
 <p>${msg}</p><button class="btn btn-primary" onclick="location.reload()">Reintentar</button>`;
 $('#loader').classList.remove('done');
}

/* ============================================================
   ARRANQUE (carga de librerías 3D)
   ============================================================ */
let THREE,OrbitControls,RoomEnvironment,EffectComposer,RenderPass,UnrealBloomPass,OutputPass;
try{
 THREE=await import('three');
 ({OrbitControls}=await import('three/addons/controls/OrbitControls.js'));
 ({RoomEnvironment}=await import('three/addons/environments/RoomEnvironment.js'));
 ({EffectComposer}=await import('three/addons/postprocessing/EffectComposer.js'));
 ({RenderPass}=await import('three/addons/postprocessing/RenderPass.js'));
 ({UnrealBloomPass}=await import('three/addons/postprocessing/UnrealBloomPass.js'));
 ({OutputPass}=await import('three/addons/postprocessing/OutputPass.js'));
}catch(e){ fatal('No se pudieron cargar las librerías 3D. Este simulador necesita conexión a internet la primera vez. Revisa la conexión y recarga la página.'); throw e; }

try{ init(); }catch(e){ console.error(e); fatal('Tu navegador no pudo crear la escena 3D (WebGL). Prueba con Chrome, Edge o Firefox actualizados.'); throw e; }

function init(){
/* ============================================================
   ESCENA, CÁMARA, LUCES
   ============================================================ */
const wrap=$('#viewport');
const renderer=new THREE.WebGLRenderer({antialias:true,alpha:false,preserveDrawingBuffer:true});
renderer.toneMapping=THREE.ACESFilmicToneMapping;
renderer.toneMappingExposure=1.05;
renderer.shadowMap.enabled=true;
renderer.shadowMap.type=THREE.PCFSoftShadowMap;
renderer.localClippingEnabled=true;
wrap.appendChild(renderer.domElement);

const scene=new THREE.Scene();
scene.fog=new THREE.Fog(0x0a1120,20,48);

/* Fondo degradado con brillos (textura en espacio de pantalla) */
{
 const c=document.createElement('canvas'); c.width=c.height=512; const g=c.getContext('2d');
 const lin=g.createLinearGradient(0,0,0,512); lin.addColorStop(0,'#0e1930'); lin.addColorStop(.55,'#0a1322'); lin.addColorStop(1,'#0b0f1a');
 g.fillStyle=lin; g.fillRect(0,0,512,512);
 let r=g.createRadialGradient(150,110,10,150,110,330); r.addColorStop(0,'rgba(70,140,255,0.20)'); r.addColorStop(1,'rgba(70,140,255,0)');
 g.fillStyle=r; g.fillRect(0,0,512,512);
 r=g.createRadialGradient(420,440,10,420,440,300); r.addColorStop(0,'rgba(255,120,60,0.14)'); r.addColorStop(1,'rgba(255,120,60,0)');
 g.fillStyle=r; g.fillRect(0,0,512,512);
 const tex=new THREE.CanvasTexture(c); tex.colorSpace=THREE.SRGBColorSpace; scene.background=tex;
}

const camera=new THREE.PerspectiveCamera(45,1,0.1,120);
camera.position.set(16,10,18);
const controls=new OrbitControls(camera,renderer.domElement);
controls.enableDamping=true; controls.dampingFactor=.07;
controls.minDistance=3.5; controls.maxDistance=32;
controls.minPolarAngle=.05; controls.maxPolarAngle=1.52;
controls.target.set(0,2.4,0);
controls.autoRotateSpeed=.7;

/* Entorno para reflejos metálicos */
{
 const pm=new THREE.PMREMGenerator(renderer);
 scene.environment=pm.fromScene(new RoomEnvironment(),.04).texture; pm.dispose();
}

/* Luces dramáticas */
scene.add(new THREE.HemisphereLight(0x9db8ff,0x2a1c14,.5));
const key=new THREE.DirectionalLight(0xfff1dd,1.7);
key.position.set(6,9,7); key.castShadow=true;
key.shadow.mapSize.set(1024,1024);
key.shadow.camera.left=key.shadow.camera.bottom=-9;
key.shadow.camera.right=key.shadow.camera.top=9;
key.shadow.camera.near=1; key.shadow.camera.far=32; key.shadow.bias=-.0005;
scene.add(key);
const rim=new THREE.DirectionalLight(0x4da3ff,1.2); rim.position.set(-7,4,-6); scene.add(rim);
const fill=new THREE.PointLight(0xff8a5a,.55,24); fill.position.set(-4,1,6); scene.add(fill);
const sparkLight=new THREE.PointLight(0xff7a30,0,8,2); sparkLight.position.set(0,3.7,.25); scene.add(sparkLight);

/* Post-procesado (bloom para chispa y combustión) */
const composer=new EffectComposer(renderer);
composer.addPass(new RenderPass(scene,camera));
const bloom=new UnrealBloomPass(new THREE.Vector2(800,600),.45,.4,.78);
composer.addPass(bloom);
composer.addPass(new OutputPass());

/* ============================================================
   MATERIALES Y UTILIDADES
   ============================================================ */
const cutPlane=new THREE.Plane(new THREE.Vector3(0,0,-1),.02);
const allMats=[],clipMats=[];
function M(opts,clip=false){
 const m=new THREE.MeshStandardMaterial(Object.assign({envMapIntensity:.55},opts));
 m.userData.baseEmissive=m.emissive.getHex(); m.userData.baseEI=m.emissiveIntensity;
 allMats.push(m);
 if(clip){clipMats.push(m); m.clippingPlanes=[cutPlane]; m.side=THREE.DoubleSide;}
 return m;
}
function mesh(geo,mat,parent,x=0,y=0,z=0,shadow=true){
 const o=new THREE.Mesh(geo,mat); o.position.set(x,y,z);
 o.castShadow=shadow; parent.add(o); return o;
}
const softTex=(()=>{ const c=document.createElement('canvas'); c.width=c.height=64; const g=c.getContext('2d');
 const r=g.createRadialGradient(32,32,0,32,32,30); r.addColorStop(0,'rgba(255,255,255,1)'); r.addColorStop(.4,'rgba(255,255,255,.6)'); r.addColorStop(1,'rgba(255,255,255,0)');
 g.fillStyle=r; g.fillRect(0,0,64,64); return new THREE.CanvasTexture(c); })();

/* Registro de piezas para despiece */
const engine=new THREE.Group(); scene.add(engine);
const parts=[];
function part(id,base,offset,posePos=null){
 const g=new THREE.Group(); g.position.copy(base); g.userData.partId=id; engine.add(g);
 const rec={id,group:g,base:base.clone(),offset:offset.clone(),pose:posePos?posePos.clone():null,mats:[]};
 parts.push(rec); return rec;
}
const V=(x,y,z)=>new THREE.Vector3(x,y,z);

/* ============================================================
   CONSTRUCCIÓN DEL MOTOR
   ============================================================ */
const R=.85,L=2.5,CHAMBER=4.14;

/* --- Cárter (5 placas + aceite) --- */
const caseRec=part('carter',V(0,-.05,0),V(0,0,0));
{
 const cm=M({color:0x46536a,metalness:.55,roughness:.6},true);
 mesh(new THREE.BoxGeometry(2.9,2.5,.12),cm,caseRec.group,0,0,-1.19,false);
 mesh(new THREE.BoxGeometry(.12,2.5,2.5),cm,caseRec.group,-1.39,0,0,false);
 mesh(new THREE.BoxGeometry(.12,2.5,2.5),cm,caseRec.group,1.39,0,0,false);
 mesh(new THREE.BoxGeometry(2.9,.14,2.5),cm,caseRec.group,0,-1.28,0,false);
 const rimM=M({color:0x556482,metalness:.6,roughness:.5},true);
 mesh(new THREE.BoxGeometry(2.9,.14,.45),rimM,caseRec.group,0,1.25,-1.02,false);
 mesh(new THREE.BoxGeometry(2.9,.14,.45),rimM,caseRec.group,0,1.25,1.02,false);
 mesh(new THREE.BoxGeometry(.45,.14,1.6),rimM,caseRec.group,-1.22,1.25,0,false);
 mesh(new THREE.BoxGeometry(.45,.14,1.6),rimM,caseRec.group,1.22,1.25,0,false);
 const oil=M({color:0xb45309,emissive:0xb45309,emissiveIntensity:.18,roughness:.3,metalness:.2,transparent:true,opacity:.9},true);
 mesh(new THREE.BoxGeometry(2.6,.06,2.2),oil,caseRec.group,0,-1.1,0,false).userData.noHL=true;
}

/* --- Cigüeñal (pivote → giro) --- */
const crankRec=part('ciguenal',V(0,0,0),V(0,1.2,0));
const crankRot=new THREE.Group(); crankRec.group.add(crankRot);
{
 const steel=M({color:0x9aa7b8,metalness:.9,roughness:.35});
 const dark=M({color:0x5b6675,metalness:.85,roughness:.45});
 const j=new THREE.CylinderGeometry(.2,.2,.55,20); j.rotateX(Math.PI/2);
 mesh(j,steel,crankRot,0,0,.85); mesh(j,steel,crankRot,0,0,-.85);
 const nose=new THREE.CylinderGeometry(.13,.13,.6,16); nose.rotateX(Math.PI/2);
 mesh(nose,steel,crankRot,0,0,1.35); mesh(nose,steel,crankRot,0,0,-1.35);
 /* contrapesos: media luna opuesta al bulón */
 const shape=new THREE.Shape(); shape.absarc(0,0,.75,Math.PI,Math.PI*2,false); shape.closePath();
 const webGeo=new THREE.ExtrudeGeometry(shape,{depth:.14,bevelEnabled:false});
 const hub=new THREE.CylinderGeometry(.4,.4,.14,24); hub.rotateX(Math.PI/2);
 for(const z of [.35,-.35]){
  mesh(webGeo,dark,crankRot,0,0,z-.07);
  mesh(hub,dark,crankRot,0,0,z);
 }
 const pin=new THREE.CylinderGeometry(.17,.17,.6,18); pin.rotateX(Math.PI/2);
 mesh(pin,steel,crankRot,0,R,0);
 const spr=new THREE.CylinderGeometry(.3,.3,.08,24); spr.rotateX(Math.PI/2);
 mesh(spr,dark,crankRot,0,0,-1.32);
 const pul=new THREE.CylinderGeometry(.4,.4,.12,24); pul.rotateX(Math.PI/2);
 mesh(pul,dark,crankRot,0,0,1.5);
}

/* --- Volante de inercia --- */
const fwRec=part('volante',V(0,0,-1.78),V(0,1.2,0));
const fwRot=new THREE.Group(); fwRec.group.add(fwRot);
{
 const fm=M({color:0x6b7688,metalness:.8,roughness:.4});
 const dm=M({color:0x2e3745,metalness:.7,roughness:.55});
 const disc=new THREE.CylinderGeometry(1.02,1.02,.2,48); disc.rotateX(Math.PI/2);
 mesh(disc,fm,fwRot);
 mesh(new THREE.TorusGeometry(1.02,.07,10,60),dm,fwRot);
 const paint=M({color:0xff7a3d,emissive:0xff7a3d,emissiveIntensity:.35,metalness:.4,roughness:.4});
 mesh(new THREE.TorusGeometry(.78,.022,8,48),paint,fwRot,0,0,.11);
 const bolt=new THREE.CylinderGeometry(.05,.05,.08,10); bolt.rotateX(Math.PI/2);
 for(let i=0;i<6;i++){const a=i/6*Math.PI*2; mesh(bolt,dm,fwRot,Math.cos(a)*.5,Math.sin(a)*.5,.12);}
}

/* --- Biela (origen en el bulón del cigüeñal) --- */
const rodRec=part('biela',V(0,R,0),V(0,0,0),V(0,2.55,0));
{
 const rm=M({color:0xb8c2d0,metalness:.9,roughness:.3});
 mesh(new THREE.TorusGeometry(.26,.09,12,28),rm,rodRec.group);
 const shaft=new THREE.CylinderGeometry(.085,.13,L-.55,12);
 const sh=mesh(shaft,rm,rodRec.group,0,L/2,0); sh.scale.z=1.7;
 mesh(new THREE.TorusGeometry(.15,.07,12,24),rm,rodRec.group,0,L,0);
 const b=new THREE.CylinderGeometry(.04,.04,.3,8);
 mesh(b,rm,rodRec.group,-.3,0,0); mesh(b,rm,rodRec.group,.3,0,0);
}

/* --- Pistón --- */
const pistRec=part('piston',V(0,R+L,0),V(0,0,0),V(0,5.65,0));
{
 const al=M({color:0xd8dee9,metalness:.9,roughness:.32});
 const ring=M({color:0x39424f,metalness:.85,roughness:.4});
 mesh(new THREE.CylinderGeometry(.78,.78,.9,40),al,pistRec.group,0,.05,0);
 mesh(new THREE.TorusGeometry(.74,.035,8,44),al,pistRec.group,0,.48,0).rotation.x=Math.PI/2;
 for(const y of [.32,.2]) mesh(new THREE.TorusGeometry(.79,.028,8,44),ring,pistRec.group,0,y,0).rotation.x=Math.PI/2;
 const pin=new THREE.CylinderGeometry(.13,.13,1.62,16); pin.rotateX(Math.PI/2);
 mesh(pin,ring,pistRec.group,0,0,0);
}

/* --- Cilindro (camisa + aletas) --- */
const blockRec=part('cilindro',V(0,2.75,0),V(0,5.0,0));
{
 const iron=M({color:0x66788e,metalness:.6,roughness:.55},true);
 mesh(new THREE.CylinderGeometry(1.12,1.12,2.8,48,1,true),iron,blockRec.group,0,0,0,false);
 mesh(new THREE.CylinderGeometry(.84,.84,2.8,48,1,true),iron,blockRec.group,0,0,0,false);
 const ringGeo=new THREE.RingGeometry(.84,1.12,48);
 const top=mesh(ringGeo,iron,blockRec.group,0,1.4,0,false); top.rotation.x=-Math.PI/2;
 const bot=mesh(ringGeo,iron,blockRec.group,0,-1.4,0,false); bot.rotation.x=-Math.PI/2;
 const finM=M({color:0x76889e,metalness:.6,roughness:.5},true);
 for(let i=0;i<5;i++) mesh(new THREE.TorusGeometry(1.19,.045,8,52),finM,blockRec.group,0,-1+i*.5,0,false).rotation.x=Math.PI/2;
}

/* --- Culata --- */
const headRec=part('culata',V(0,4.65,0),V(0,6.5,0));
{
 const hm=M({color:0x7e8fa6,metalness:.7,roughness:.45},true);
 mesh(new THREE.BoxGeometry(2.5,1,2.1),hm,headRec.group,0,0,0,false);
 const finM=M({color:0x8b9cb4,metalness:.7,roughness:.4},true);
 for(const y of [.12,.3,.48]) mesh(new THREE.BoxGeometry(2.64,.06,2.22),finM,headRec.group,0,y,0,false);
 const guide=new THREE.CylinderGeometry(.09,.09,.5,12);
 mesh(guide,hm,headRec.group,-.42,.7,0,false); mesh(guide,hm,headRec.group,.42,.7,0,false);
 mesh(new THREE.CylinderGeometry(.16,.16,.3,14),hm,headRec.group,0,.55,0,false);
 const standM=M({color:0x5b6b84,metalness:.7,roughness:.5},true);
 for(const x of [-.42,.42]) for(const z of [-.8,.8])
  mesh(new THREE.BoxGeometry(.14,.9,.14),standM,headRec.group,x,.95,z,false);
}

/* --- Válvulas --- */
function buildValve(id,x,color){
 const rec=part(id,V(x,4.2,0),V(id==='valvula_admision'?-.35:.35,7.6,0));
 const vm=M({color,metalness:.9,roughness:.28});
 mesh(new THREE.CylinderGeometry(.3,.3,.06,28),vm,rec.group,0,0,0);
 mesh(new THREE.CylinderGeometry(.1,.27,.13,20),vm,rec.group,0,.09,0);
 mesh(new THREE.CylinderGeometry(.055,.055,1.7,12),vm,rec.group,0,.85,0);
 const sm=M({color:0x8a94a6,metalness:.85,roughness:.4});
 for(const y of [1.12,1.25,1.38,1.51]) mesh(new THREE.TorusGeometry(.11,.018,8,20),sm,rec.group,0,y,0).rotation.x=Math.PI/2;
 mesh(new THREE.CylinderGeometry(.14,.14,.05,14),sm,rec.group,0,1.58,0);
 return rec;
}
const valveIn=buildValve('valvula_admision',-.42,0x9fc4e8);
const valveEx=buildValve('valvula_escape',.42,0xd8a08a);

/* --- Árboles de levas (2 levas, giran a mitad de velocidad) --- */
function buildCam(x,phase){
 const rec=part('arbol_levas',V(x,6.12,0),V(x<0?-.25:.25,8.5,0));
 const rot=new THREE.Group(); rec.group.add(rot);
 const cm=M({color:0x8a94a6,metalness:.9,roughness:.35});
 const lm=M({color:0xc084fc,metalness:.75,roughness:.35,emissive:0x7c3aed,emissiveIntensity:.12});
 const shaft=new THREE.CylinderGeometry(.11,.11,1.9,14); shaft.rotateX(Math.PI/2);
 mesh(shaft,cm,rot);
 const base=new THREE.CylinderGeometry(.17,.17,.28,20); base.rotateX(Math.PI/2);
 mesh(base,lm,rot);
 const nose=mesh(new THREE.SphereGeometry(.155,16,12),lm,rot,0,.14,0); nose.scale.set(1,1.55,.9);
 const spr=new THREE.CylinderGeometry(.28,.28,.07,24); spr.rotateX(Math.PI/2);
 mesh(spr,cm,rot,0,0,-1.32);
 mesh(new THREE.TorusGeometry(.28,.03,8,28),cm,rot,0,0,-1.32);
 return {rec,rot,phase};
}
const camIn=buildCam(-.42,225*RAD);
const camEx=buildCam(.42,135*RAD);

/* --- Bujía + destello de chispa --- */
const plugRec=part('bujia',V(0,4.2,0),V(0,8.0,0));
let sparkSprite;
{
 const cu=M({color:0xd98a4a,metalness:.9,roughness:.3});
 const st=M({color:0x9aa7b8,metalness:.9,roughness:.35});
 const ce=M({color:0xf2f0e9,metalness:.1,roughness:.4});
 mesh(new THREE.CylinderGeometry(.03,.03,.18,8),cu,plugRec.group,0,-.02,0);
 mesh(new THREE.CylinderGeometry(.11,.11,.35,14),st,plugRec.group,0,.3,0);
 mesh(new THREE.CylinderGeometry(.16,.16,.18,6),st,plugRec.group,0,.55,0);
 mesh(new THREE.CylinderGeometry(.12,.12,.7,14),ce,plugRec.group,0,1,0);
 mesh(new THREE.CylinderGeometry(.05,.05,.16,10),st,plugRec.group,0,1.44,0);
 mesh(new THREE.SphereGeometry(.07,12,10),st,plugRec.group,0,1.54,0);
 sparkSprite=new THREE.Sprite(new THREE.SpriteMaterial({map:softTex,color:0xcfe8ff,transparent:true,opacity:0,depthWrite:false,blending:THREE.AdditiveBlending}));
 sparkSprite.position.set(0,-.1,0); sparkSprite.scale.setScalar(.6);
 sparkSprite.userData.noPick=true; plugRec.group.add(sparkSprite);
}

/* --- Conductos de admisión y escape --- */
const inCurve=new THREE.CatmullRomCurve3([V(-2.7,4.95,0),V(-2.1,4.95,0),V(-1.35,4.85,0),V(-.75,4.55,0),V(-.42,4.3,0),V(-.42,3.7,0)]);
const exCurve=new THREE.CatmullRomCurve3([V(.42,3.75,0),V(.42,4.3,0),V(.75,4.55,0),V(1.35,4.85,0),V(2.1,4.95,0),V(2.7,4.95,0),V(3.3,5.05,0)]);
const portInRec=part('conducto_admision',V(0,0,0),V(-1.2,6.5,0));
const portExRec=part('conducto_escape',V(0,0,0),V(1.2,6.5,0));
{
 const im=M({color:0x3d7fb8,metalness:.7,roughness:.4},true);
 mesh(new THREE.TubeGeometry(inCurve,32,.22,12,false),im,portInRec.group,0,0,0,false);
 const flare=new THREE.CylinderGeometry(.3,.24,.28,18); flare.rotateZ(Math.PI/2);
 mesh(flare,M({color:0x4cc9f0,metalness:.8,roughness:.3},true),portInRec.group,-2.78,4.95,0,false);
 const inj=new THREE.CylinderGeometry(.05,.07,.3,10);
 const injM=mesh(inj,M({color:0xd98a4a,metalness:.9,roughness:.3}),portInRec.group,-1.05,4.95,0); injM.rotation.z=.5;
 const em=M({color:0xb08a7a,metalness:.75,roughness:.45},true);
 mesh(new THREE.TubeGeometry(exCurve,32,.21,12,false),em,portExRec.group,0,0,0,false);
 const flare2=new THREE.CylinderGeometry(.28,.22,.3,18); flare2.rotateZ(Math.PI/2);
 mesh(flare2,M({color:0x6b5a52,metalness:.7,roughness:.5},true),portExRec.group,3.35,5.06,0,false);
}

/* --- Correa de distribución --- */
const beltRec=part('correa',V(0,0,0),V(0,0,0));
const beltMat=M({color:0x232a36,metalness:.1,roughness:.9,transparent:true,opacity:1});
{
 const pts=[V(.34,-.1,-1.34),V(.5,3,-1.34),V(.72,6,-1.34),V(.42,6.45,-1.34),V(-.42,6.45,-1.34),V(-.72,6,-1.34),V(-.5,3,-1.34),V(-.34,-.1,-1.34),V(0,-.42,-1.34)];
 const curve=new THREE.CatmullRomCurve3(pts,true);
 mesh(new THREE.TubeGeometry(curve,80,.055,8,true),beltMat,beltRec.group,0,0,0,false);
 const rib=M({color:0xa3e635,metalness:.2,roughness:.7,emissive:0x4d7c0f,emissiveIntensity:.2,transparent:true,opacity:1});
 beltRec.userData=beltRec.userData||{}; beltRec.ribMat=rib;
 mesh(new THREE.TubeGeometry(curve,80,.02,6,true),rib,beltRec.group,0,0,.045,false);
}

/* --- Gas dentro del cilindro (visualización del ciclo) --- */
const gasMat=new THREE.MeshStandardMaterial({color:0x38bdf8,emissive:0x38bdf8,emissiveIntensity:.3,
 transparent:true,opacity:.25,depthWrite:false,side:THREE.DoubleSide,clippingPlanes:[cutPlane],roughness:1,metalness:0});
const gas=new THREE.Mesh(new THREE.CylinderGeometry(.8,.8,1,36,1,false),gasMat);
gas.userData.noPick=true; gas.castShadow=false; scene.add(gas);

/* --- Plataforma y pedestal (no son piezas del motor) --- */
{
 const plat=new THREE.Mesh(new THREE.CylinderGeometry(6.5,6.8,.14,64),
  new THREE.MeshStandardMaterial({color:0x0d1728,roughness:.95,metalness:.1}));
 plat.position.y=-2.27; plat.receiveShadow=true; scene.add(plat);
 const ring=new THREE.Mesh(new THREE.TorusGeometry(6.3,.03,8,90),
  new THREE.MeshStandardMaterial({color:0x3b82f6,emissive:0x3b82f6,emissiveIntensity:.8,roughness:.5}));
 ring.rotation.x=Math.PI/2; ring.position.y=-2.19; scene.add(ring);
 const grid=new THREE.GridHelper(34,34,0x1c2c48,0x131f36); grid.position.y=-2.33; scene.add(grid);
 const ped=new THREE.Mesh(new THREE.BoxGeometry(1.9,.85,1.5),
  new THREE.MeshStandardMaterial({color:0x1a2436,roughness:.7,metalness:.4}));
 ped.position.y=-1.78; ped.castShadow=true; scene.add(ped);
 const stripe=new THREE.Mesh(new THREE.BoxGeometry(1.9,.07,.03),
  new THREE.MeshStandardMaterial({color:0xff7a3d,emissive:0xff7a3d,emissiveIntensity:.5}));
 stripe.position.set(0,-1.5,.76); scene.add(stripe);
}

/* Recopilar materiales por pieza (para resaltado) */
for(const p of parts){
 p.group.traverse(o=>{ if(o.isMesh && !o.userData.noHL){ o.userData.partId=p.id; if(!p.mats.includes(o.material)) p.mats.push(o.material);} });
}
const pickables=[];
engine.traverse(o=>{ if(o.isMesh && !o.userData.noPick) pickables.push(o); });

/* ============================================================
   PARTÍCULAS (flujo de gases + polvo ambiental)
   ============================================================ */
function makeFlow(curve,color,max,size,op){
 const geo=new THREE.BufferGeometry();
 const pos=new Float32Array(max*3); pos.fill(-999);
 geo.setAttribute('position',new THREE.BufferAttribute(pos,3));
 const mat=new THREE.PointsMaterial({map:softTex,color,size,transparent:true,opacity:op,depthWrite:false,blending:THREE.AdditiveBlending});
 const pts=new THREE.Points(geo,mat); pts.frustumCulled=false; scene.add(pts);
 return {curve,geo,pos,mat,list:[],max,acc:0,pts};
}
const flowIn=makeFlow(inCurve,0x8fd8ff,90,.11,.85);
const flowEx=makeFlow(exCurve,0xb9c4cf,90,.13,.5);
function updateFlow(f,dt,open,e){
 const speedScale=.5+state.rpm/110;
 if(open>.06 && state.playing && e<.3){
  f.acc+=dt*(16+state.rpm*.35)*open;
  while(f.acc>=1 && f.list.length<f.max){ f.acc--; f.list.push({t:0,sp:.8+Math.random()*.5,jx:(Math.random()-.5)*.14,jy:(Math.random()-.5)*.14,jz:(Math.random()-.5)*.2}); }
  if(f.acc>1) f.acc=1;
 }
 let n=0; const v=new THREE.Vector3();
 for(let i=f.list.length-1;i>=0;i--){
  const p=f.list[i]; p.t+=p.sp*speedScale*dt;
  if(p.t>=1){ f.list.splice(i,1); continue; }
  f.curve.getPointAt(p.t,v);
  f.pos[n*3]=v.x+p.jx*p.t; f.pos[n*3+1]=v.y+p.jy*p.t; f.pos[n*3+2]=v.z+p.jz; n++;
 }
 for(let i=n;i<f.max;i++){ f.pos[i*3+1]=-999; }
 f.geo.setDrawRange(0,n); f.geo.attributes.position.needsUpdate=true;
 f.mat.opacity=(f===flowIn?.85:.5)*(1-e);
}
/* Polvo ambiental */
const DUST_MAX=120;
const dustGeo=new THREE.BufferGeometry();
const dustPos=new Float32Array(DUST_MAX*3); const dustSeed=[];
for(let i=0;i<DUST_MAX;i++){ dustSeed.push({x:(Math.random()-.5)*16,y:-2+Math.random()*11,z:(Math.random()-.5)*16,s:Math.random()*6.28,v:.1+Math.random()*.2}); }
dustGeo.setAttribute('position',new THREE.BufferAttribute(dustPos,3));
const dust=new THREE.Points(dustGeo,new THREE.PointsMaterial({map:softTex,color:0x7fb2ff,size:.06,transparent:true,opacity:.3,depthWrite:false,blending:THREE.AdditiveBlending}));
dust.frustumCulled=false; scene.add(dust);
let dustCount=80;

/* ============================================================
   SONIDO PROCEDURAL (WebAudio)
   ============================================================ */
const S={ctx:null,master:null,humOsc:null,humGain:null,noiseBuf:null};
function soundEnsure(){
 if(!S.ctx){
  try{
   const ctx=new (window.AudioContext||window.webkitAudioContext)(); S.ctx=ctx;
   S.master=ctx.createGain(); S.master.gain.value=state.sound?.5:0; S.master.connect(ctx.destination);
   const buf=ctx.createBuffer(1,ctx.sampleRate,ctx.sampleRate);
   const d=buf.getChannelData(0); for(let i=0;i<d.length;i++) d[i]=Math.random()*2-1; S.noiseBuf=buf;
   S.humOsc=ctx.createOscillator(); S.humOsc.type='sawtooth'; S.humOsc.frequency.value=40;
   const lp=ctx.createBiquadFilter(); lp.type='lowpass'; lp.frequency.value=240;
   S.humGain=ctx.createGain(); S.humGain.gain.value=0;
   S.humOsc.connect(lp); lp.connect(S.humGain); S.humGain.connect(S.master); S.humOsc.start();
  }catch(e){}
 }
 if(S.ctx && S.ctx.state==='suspended') S.ctx.resume();
}
function soundPop(){
 if(!S.ctx||!state.sound) return; const ctx=S.ctx,t=ctx.currentTime;
 const src=ctx.createBufferSource(); src.buffer=S.noiseBuf;
 const bp=ctx.createBiquadFilter(); bp.type='bandpass'; bp.frequency.value=260; bp.Q.value=.9;
 const g=ctx.createGain(); g.gain.setValueAtTime(.55,t); g.gain.exponentialRampToValueAtTime(.001,t+.12);
 src.connect(bp); bp.connect(g); g.connect(S.master); src.start(t); src.stop(t+.13);
 const o=ctx.createOscillator(); o.type='sine'; o.frequency.setValueAtTime(95,t); o.frequency.exponentialRampToValueAtTime(38,t+.18);
 const og=ctx.createGain(); og.gain.setValueAtTime(.5,t); og.gain.exponentialRampToValueAtTime(.001,t+.2);
 o.connect(og); og.connect(S.master); o.start(t); o.stop(t+.22);
}
function soundWhoosh(exhaust){
 if(!S.ctx||!state.sound||!state.playing) return; const ctx=S.ctx,t=ctx.currentTime;
 const src=ctx.createBufferSource(); src.buffer=S.noiseBuf; src.loop=true;
 const bp=ctx.createBiquadFilter(); bp.type='bandpass'; bp.frequency.value=exhaust?420:900; bp.Q.value=.7;
 const g=ctx.createGain(); const dur=clamp(90/Math.max(state.rpm,20),.15,.6);
 g.gain.setValueAtTime(.0001,t); g.gain.exponentialRampToValueAtTime(exhaust?.09:.12,t+dur*.3); g.gain.exponentialRampToValueAtTime(.001,t+dur);
 src.connect(bp); bp.connect(g); g.connect(S.master); src.start(t); src.stop(t+dur+.05);
}
function soundUpdate(){
 if(!S.ctx) return;
 S.humOsc.frequency.setTargetAtTime(18+state.rpm*.5,S.ctx.currentTime,.1);
 S.humGain.gain.setTargetAtTime(state.playing?.03+state.rpm*.00028:0,S.ctx.currentTime,.15);
}
window.addEventListener('pointerdown',soundEnsure,{once:true});
window.addEventListener('keydown',soundEnsure,{once:true});

/* ============================================================
   ETIQUETAS HTML (en español) + LÍNEAS GUÍA
   ============================================================ */
const labelsLayer=$('#labelsLayer'),leaderSvg=$('#leaderSvg');
const labelRecs=[];
function addLabel(id,parent,local,dx,dy){
 const anchor=new THREE.Object3D(); anchor.position.copy(local); parent.add(anchor);
 const color=PARTS[id].color;
 const pill=document.createElement('button'); pill.className='pill'; pill.style.setProperty('--pc',color);
 pill.innerHTML=`<i></i>${PARTS[id].name}`; pill.dataset.part=id;
 pill.addEventListener('click',ev=>{ev.stopPropagation(); selectPart(state.selected===id?null:id);});
 labelsLayer.appendChild(pill);
 const ns='http://www.w3.org/2000/svg';
 const line=document.createElementNS(ns,'line'); line.setAttribute('stroke',color); line.setAttribute('stroke-width','1'); line.setAttribute('opacity','.55');
 const dot=document.createElementNS(ns,'circle'); dot.setAttribute('r','3'); dot.setAttribute('fill',color);
 leaderSvg.appendChild(line); leaderSvg.appendChild(dot);
 labelRecs.push({id,anchor,pill,line,dot,dx,dy});
}
addLabel('bujia',plugRec.group,V(0,1.3,0),0,-46);
addLabel('valvula_admision',valveIn.group,V(0,.6,0),-72,-32);
addLabel('valvula_escape',valveEx.group,V(0,.6,0),72,-32);
addLabel('arbol_levas',camIn.rec.group,V(0,.25,0),-88,-24);
addLabel('piston',pistRec.group,V(.5,.3,0),80,-6);
addLabel('biela',rodRec.group,V(0,L*.55,0),-84,10);
addLabel('ciguenal',crankRec.group,V(0,-.55,.4),-92,38);
addLabel('volante',fwRec.group,V(0,-.9,0),-66,46);
addLabel('cilindro',blockRec.group,V(1,.6,.3),96,-12);
addLabel('culata',headRec.group,V(1.1,.3,0),96,-30);
addLabel('carter',caseRec.group,V(-1.3,-.6,.4),-92,28);
addLabel('conducto_admision',portInRec.group,V(-2.3,4.95,0),-64,-40);
addLabel('conducto_escape',portExRec.group,V(2.3,4.95,0),64,-40);
addLabel('correa',beltRec.group,V(-.62,3,-1.34),-64,12);

let vw=800,vh=600;
const projV=new THREE.Vector3();
function updateLabels(){
 if(!state.labels){ labelsLayer.style.display='none'; return; }
 labelsLayer.style.display='block';
 for(const r of labelRecs){
  let op=1;
  if(r.id==='correa') op=clamp(1-state.explode*1.6,0,1);
  r.anchor.getWorldPosition(projV); projV.project(camera);
  const behind=projV.z>1;
  const x=(projV.x*.5+.5)*vw, y=(-projV.y*.5+.5)*vh;
  const off=behind||x<-60||x>vw+60||y<-40||y>vh+40||op<=.02;
  r.pill.style.display=off?'none':'flex';
  r.line.style.display=r.dot.style.display=off?'none':'block';
  if(off) continue;
  r.pill.style.opacity=op; r.line.setAttribute('opacity',.55*op); r.dot.setAttribute('opacity',op);
  const px=x+r.dx, py=y+r.dy;
  r.pill.style.transform=`translate(${px}px,${py}px) translate(-50%,-50%)`;
  r.line.setAttribute('x1',x); r.line.setAttribute('y1',y); r.line.setAttribute('x2',px); r.line.setAttribute('y2',py);
  r.dot.setAttribute('cx',x); r.dot.setAttribute('cy',y);
  r.pill.classList.toggle('active',state.selected===r.id);
 }
}

/* ============================================================
   SELECCIÓN / RESALTADO DE PIEZAS
   ============================================================ */
const raycaster=new THREE.Raycaster(); const pointer=new THREE.Vector2();
let pointerMoved=false,downPos=null,downTime=0;
function restoreMats(rec){ for(const m of rec.mats){ m.emissive.setHex(m.userData.baseEmissive); m.emissiveIntensity=m.userData.baseEI; } }
function selectPart(id){
 if(state.selected){ const old=parts.find(p=>p.id===state.selected); if(old) restoreMats(old); }
 state.selected=id;
 document.querySelectorAll('.chip').forEach(c=>c.classList.toggle('active',c.dataset.part===id));
 const card=$('#infoCard');
 if(id){
  const p=PARTS[id];
  card.style.setProperty('--ic',p.color);
  $('#infoName').textContent=p.name; $('#infoDesc').textContent=p.desc;
  card.classList.add('show');
 }else card.classList.remove('show');
}
$('#infoClose').addEventListener('click',()=>selectPart(null));
function pickAt(cx,cy){
 const rect=renderer.domElement.getBoundingClientRect();
 pointer.x=((cx-rect.left)/rect.width)*2-1; pointer.y=-((cy-rect.top)/rect.height)*2+1;
 raycaster.setFromCamera(pointer,camera);
 const hits=raycaster.intersectObjects(pickables,false);
 for(const h of hits){ if(!h.object.visible) continue;
  let o=h.object; while(o && !o.userData.partId) o=o.parent;
  if(o) return o.userData.partId;
 }
 return null;
}
renderer.domElement.addEventListener('pointerdown',e=>{downPos=[e.clientX,e.clientY];downTime=performance.now();});
renderer.domElement.addEventListener('pointerup',e=>{
 if(!downPos) return;
 const d=Math.hypot(e.clientX-downPos[0],e.clientY-downPos[1]);
 if(d<6 && performance.now()-downTime<450){ const id=pickAt(e.clientX,e.clientY); selectPart(id===state.selected?null:id); }
 downPos=null;
});
let lastMove=null;
renderer.domElement.addEventListener('pointermove',e=>{lastMove=[e.clientX,e.clientY];pointerMoved=true;});
function updateHover(t){
 if(pointerMoved && lastMove){
  pointerMoved=false;
  const id=pickAt(lastMove[0],lastMove[1]);
  if(id!==state.hovered){
   if(state.hovered && state.hovered!==state.selected){ const old=parts.find(p=>p.id===state.hovered); if(old) restoreMats(old); }
   state.hovered=id;
   renderer.domElement.style.cursor=id?'pointer':'grab';
   if(id && id!==state.selected){ const rec=parts.find(p=>p.id===id);
    for(const m of rec.mats){ m.emissive.set(PARTS[id].color); m.emissiveIntensity=.16; } }
  }
 }
 if(state.selected){
  const rec=parts.find(p=>p.id===state.selected);
  const pulse=.32+.22*Math.sin(t*5.5);
  for(const m of rec.mats){ m.emissive.set(PARTS[state.selected].color); m.emissiveIntensity=pulse; }
 }
}

/* ============================================================
   INTERFAZ: BINDINGS
   ============================================================ */
function setRange(el){ el.style.setProperty('--p',((el.value-el.min)/(el.max-el.min)*100)+'%'); }
document.querySelectorAll('input[type=range]').forEach(setRange);

function syncPlayUI(){
 $('#icPause').style.display=state.playing?'block':'none';
 $('#icPlay').style.display=state.playing?'none':'block';
 $('#playLabel').textContent=state.playing?'Pausar':'Reproducir';
}
$('#playBtn').addEventListener('click',()=>{state.playing=!state.playing;state.stepMode=false;syncPlayUI();});

let angleTween=null;
function tweenAngle(to,dur,step=false){
 state.stepMode=step; if(step){state.playing=false;syncPlayUI();}
 angleTween={from:state.angle,to,start:performance.now(),dur:dur*1000};
}
$('#stepBtn').addEventListener('click',()=>{
 const next=(Math.floor(state.angle/180)+1)*180;
 tweenAngle(next>=720?719.99:next,1.1,true);
 toast('Avanzando un tiempo completo (180°)');
});
document.querySelectorAll('.tl-seg').forEach(b=>b.addEventListener('click',()=>{
 tweenAngle(parseInt(b.dataset.i)*180+.01,.7,false);
}));

$('#rpmSlider').addEventListener('input',e=>{
 state.rpm=parseInt(e.target.value); setRange(e.target);
 $('#rpmOut').textContent=state.rpm+' RPM'; $('#rpmTxt').textContent=state.rpm+' RPM';
});

function syncExplodeUI(){
 const armed=state.explodeTarget>.5;
 $('#explodeBtn').classList.toggle('armed',armed);
 $('#explodeBtn').setAttribute('aria-pressed',armed);
 $('#explodeLabel').textContent=armed?'ARMAR EL MOTOR':'DESPIECE DEL MOTOR';
}
$('#explodeBtn').addEventListener('click',()=>{
 const to=state.explodeTarget>.5?0:1;
 if(to===1){ state.wasPlaying=state.playing; state.playing=false; syncPlayUI(); toast('Despiece: piezas separadas y numeradas por color'); }
 else { state.playing=state.wasPlaying; syncPlayUI(); toast('Motor armado de nuevo'); }
 state.explodeTarget=to; syncExplodeUI();
});
$('#sepSlider').addEventListener('input',e=>{
 const v=parseInt(e.target.value)/100; setRange(e.target);
 state.explode=v; state.explodeTarget=v;
 $('#sepOut').textContent=Math.round(v*100)+'%'; syncExplodeUI();
});

function applyCut(){
 for(const m of clipMats){ m.clippingPlanes=state.cutaway?[cutPlane]:null; m.needsUpdate=true; }
 gasMat.clippingPlanes=state.cutaway?[cutPlane]:null; gasMat.needsUpdate=true;
}
$('#cutToggle').addEventListener('change',e=>{state.cutaway=e.target.checked;applyCut();toast(state.cutaway?'Corte transversal activado':'Motor completo (sin corte)');});
$('#labelsToggle').addEventListener('change',e=>{state.labels=e.target.checked;});
$('#rotToggle').addEventListener('change',e=>{state.autoRot=e.target.checked;controls.autoRotate=state.autoRot;});

function applyQuality(){
 const q=state.quality;
 const dpr=q==='alta'?Math.min(devicePixelRatio,2):q==='media'?Math.min(devicePixelRatio,1.5):1;
 renderer.setPixelRatio(dpr); composer.setPixelRatio(dpr);
 bloom.enabled=q!=='baja'; bloom.strength=q==='alta'?.5:.4;
 const sh=q!=='baja'; renderer.shadowMap.enabled=sh; key.castShadow=sh;
 const size=q==='alta'?2048:1024;
 if(key.shadow.map){key.shadow.map.dispose();key.shadow.map=null;}
 key.shadow.mapSize.set(size,size);
 dustCount=q==='alta'?120:q==='media'?80:40;
 for(const m of allMats) m.needsUpdate=true;
 resize();
}
$('#qualitySel').addEventListener('change',e=>{state.quality=e.target.value;applyQuality();toast('Calidad: '+e.target.selectedOptions[0].text);});

/* Cámara */
let camTween=null;
function camTo(pos,target,dur=.9){
 camTween={fp:camera.position.clone(),tp:pos.clone(),ft:controls.target.clone(),tt:target.clone(),start:performance.now(),dur:dur*1000};
}
controls.addEventListener('start',()=>{camTween=null;});
const explodeY=()=>2.4+3.8*state.explode;
const views={
 front:()=>camTo(V(0,explodeY()+.8,12.5+9*state.explode),V(0,explodeY(),0)),
 side:()=>camTo(V(12.5+9*state.explode,explodeY()+1,.5),V(0,explodeY(),0)),
 top:()=>camTo(V(.5,explodeY()+13+7*state.explode,.5),V(0,explodeY(),0)),
 iso:()=>camTo(V(6.8,explodeY()+2.5,10.2+7*state.explode),V(0,explodeY(),0))
};
document.querySelectorAll('.cam-btn').forEach(b=>b.addEventListener('click',()=>views[b.dataset.view]()));
$('#centerBtn').addEventListener('click',()=>views.iso());
$('#randomBtn').addEventListener('click',()=>{
 const az=Math.random()*Math.PI*2,pol=.35+Math.random()*.9,d=9+Math.random()*8+8*state.explode;
 const ty=explodeY();
 camTo(V(Math.sin(az)*Math.sin(pol)*d,ty+Math.cos(pol)*d,Math.cos(az)*Math.sin(pol)*d),V(0,ty,0));
 toast('¡Vista sorpresa! 🎲');
});

/* Sonido / pantalla completa */
function syncSoundUI(){
 $('#soundBtn').classList.toggle('off',!state.sound);
 $('#soundBtn').setAttribute('aria-pressed',state.sound);
 $('#soundLabel').textContent=state.sound?'Sonido':'Silencio';
 if(S.ctx) S.master.gain.setTargetAtTime(state.sound?.5:0,S.ctx.currentTime,.05);
}
$('#soundBtn').addEventListener('click',()=>{soundEnsure();state.sound=!state.sound;syncSoundUI();toast(state.sound?'Sonido activado 🔊':'Sonido silenciado 🔇');});
$('#fsBtn').addEventListener('click',()=>{
 try{ if(!document.fullscreenElement) document.documentElement.requestFullscreen(); else document.exitFullscreen(); }catch(e){}
});

/* Reiniciar / captura */
$('#resetBtn').addEventListener('click',resetAll);
function resetAll(){
 state.angle=0;state.cycles=0;state.rpm=50;state.playing=true;state.stepMode=false;
 state.explode=0;state.explodeTarget=0;state.cutaway=true;state.labels=true;state.autoRot=false;
 angleTween=null; selectPart(null);
 $('#rpmSlider').value=50;setRange($('#rpmSlider'));$('#rpmOut').textContent='50 RPM';$('#rpmTxt').textContent='50 RPM';
 $('#sepSlider').value=0;setRange($('#sepSlider'));$('#sepOut').textContent='0%';
 $('#cutToggle').checked=true;$('#labelsToggle').checked=true;$('#rotToggle').checked=false;
 controls.autoRotate=false; applyCut(); syncPlayUI(); syncExplodeUI();
 camTo(V(6.8,4.9,10.2),V(0,2.4,0));
 toast('Simulador reiniciado ⟳');
}
$('#shotBtn').addEventListener('click',()=>{
 try{
  const a=document.createElement('a'); a.download='motor-4-tiempos.png';
  a.href=renderer.domElement.toDataURL('image/png'); a.click();
  const f=$('#flash'); f.classList.add('on'); setTimeout(()=>f.classList.remove('on'),180);
  toast('Imagen PNG descargada 📸');
 }catch(e){ toast('No se pudo generar la captura'); }
});

/* Leyenda */
{
 const lg=$('#legend');
 for(const id of LEGEND_ORDER){
  const b=document.createElement('button'); b.className='chip'; b.dataset.part=id;
  b.style.setProperty('--pc',PARTS[id].color);
  b.innerHTML=`<i></i><span>${PARTS[id].name}</span>`;
  b.addEventListener('click',()=>selectPart(state.selected===id?null:id));
  lg.appendChild(b);
 }
}

/* Atajos de teclado */
window.addEventListener('keydown',e=>{
 if(/INPUT|SELECT|TEXTAREA/.test(e.target.tagName)) return;
 switch(e.key){
  case ' ': e.preventDefault(); $('#playBtn').click(); break;
  case 'e': case 'E': $('#explodeBtn').click(); break;
  case 'ArrowRight': $('#stepBtn').click(); break;
  case 'c': case 'C': $('#cutToggle').checked=!$('#cutToggle').checked; $('#cutToggle').dispatchEvent(new Event('change')); break;
  case 'l': case 'L': $('#labelsToggle').checked=!$('#labelsToggle').checked; $('#labelsToggle').dispatchEvent(new Event('change')); break;
  case 'r': case 'R': resetAll(); break;
  case 'Escape': selectPart(null); break;
 }
});

/* ============================================================
   HUD (insignia, tarjeta, línea de tiempo)
   ============================================================ */
let lastStroke=-1;
const segEls=[...document.querySelectorAll('.tl-seg')];
function updateStrokeUI(i){
 const s=STROKES[i];
 const badge=$('#strokeBadge');
 badge.style.setProperty('--sc',s.color);
 $('#badgeNum').textContent=i+1;
 $('#badgeName').childNodes[0].textContent=s.name.toUpperCase();
 $('#badgeSub').textContent=`Tiempo ${i+1} de 4 · ${s.motion}`;
 badge.classList.remove('pop'); void badge.offsetWidth; badge.classList.add('pop');
 const card=$('#strokeCard'); card.style.setProperty('--sc',s.color);
 $('#scNum').textContent=i+1; $('#scName').textContent=s.name; $('#scSub').textContent=s.sub;
 $('#scDesc').textContent=s.desc; $('#scTip').textContent=s.tip;
 segEls.forEach((el,j)=>{ el.classList.toggle('active',j===i); el.classList.toggle('done',j<i); });
 if(lastStroke!==-1){ if(i===0) soundWhoosh(false); if(i===3) soundWhoosh(true); }
 lastStroke=i;
}
function updateHUD(){
 const a=state.angle,i=Math.floor(a/180)%4;
 if(i!==lastStroke) updateStrokeUI(i);
 const intra=(a%180)/180;
 segEls[i].querySelector('.tl-fill').style.transform=`scaleX(${intra})`;
 $('#tlMarker').style.left=(a/720*100)+'%';
 $('#angleTxt').textContent=Math.round(a)+'°';
 $('#lapTxt').textContent=a<360?'1':'2';
 $('#cyclesTxt').textContent=state.cycles;
 const dead=$('#deadChip'); const m=a%180;
 if(m<5||m>175){ dead.style.visibility='visible'; dead.textContent=(Math.round(a/180)%2===0)?'PMS':'PMI'; }
 else dead.style.visibility='hidden';
}

/* ============================================================
   CINEMÁTICA Y BUCLE PRINCIPAL
   ============================================================ */
function setAngle(a){
 const prev=state.angle;
 a=((a%720)+720)%720;
 const crossed=prev<a?(prev<360&&a>=360):(prev<360||a>=360);
 if(prev>a) state.cycles++;
 state.angle=a;
 if(crossed && state.explode<.3) soundPop();
}
const liftProfile=(a,s,e)=>(a>=s&&a<=e)?Math.pow(Math.sin(Math.PI*(a-s)/(e-s)),1.2):0;
const cA=new THREE.Color(),cB=new THREE.Color();
const tmpV=new THREE.Vector3();

function applyKinematics(t){
 const e=smooth(clamp(state.explode,0,1));
 const th=state.angle*RAD,s=Math.sin(th),c=Math.cos(th);
 const pinX=R*s,pinY=R*c;
 const pistY=pinY+Math.sqrt(L*L-pinX*pinX);

 for(const p of parts){
  if(p.id==='biela'||p.id==='piston') continue;
  p.group.position.copy(p.base).addScaledVector(p.offset,e);
 }
 crankRot.rotation.z=-th;
 fwRot.rotation.z=-th;
 fwRec.group.position.z=-1.78-1.3*e;

 rodRec.group.position.set(lerp(pinX,0,e),lerp(pinY,2.55,e),0);
 rodRec.group.rotation.z=Math.asin(pinX/L)*(1-e);
 pistRec.group.position.set(0,lerp(pistY,5.65,e),0);

 const li=liftProfile(state.angle,0,180)*.28*(1-e);
 const le=liftProfile(state.angle,540,720)*.28*(1-e);
 valveIn.group.position.y=4.2-li+7.6*e;
 valveEx.group.position.y=4.2-le+7.6*e;
 camIn.rot.rotation.z=-th/2+camIn.phase;
 camEx.rot.rotation.z=-th/2+camEx.phase;

 const bop=clamp(1-e*1.6,0,1);
 beltMat.opacity=bop; beltRec.ribMat.opacity=bop;
 beltRec.group.visible=e<.62;

 /* Gas del ciclo */
 const a=state.angle;
 const pTop=pistY+.5, h=Math.max(.06,CHAMBER-pTop);
 gas.scale.y=h; gas.position.set(0,pTop+h/2,0);
 let glow=0;
 if(a>=355&&a<520) glow=a<360?(a-355)/5:Math.exp(-(a-360)/70);
 if(a<180){ const p=a/180; cA.set(0x7dd3fc); cB.set(0x38bdf8); gasMat.color.lerpColors(cA,cB,p);
  gasMat.emissive.copy(gasMat.color); gasMat.emissiveIntensity=.25; gasMat.opacity=.1+.25*p; }
 else if(a<360){ const p=(a-180)/180; cA.set(0x38bdf8); cB.set(0xfcd34d); gasMat.color.lerpColors(cA,cB,p);
  gasMat.emissive.copy(gasMat.color); gasMat.emissiveIntensity=.3+.4*p+glow*2.5; gasMat.opacity=.35+.3*p; }
 else if(a<540){ const p=(a-360)/180; cA.set(0xff7a33); cB.set(0xb45309); gasMat.color.lerpColors(cA,cB,p);
  cA.set(0xffffff); gasMat.emissive.lerpColors(cA,cB.set(0xff5a1f),clamp(p*2.2,0,1));
  gasMat.emissiveIntensity=.5+glow*3.2; gasMat.opacity=.75-.4*p; }
 else { const p=(a-540)/180; gasMat.color.set(0x9aa5b1); gasMat.emissive.set(0x6b7480);
  gasMat.emissiveIntensity=.15; gasMat.opacity=.35*(1-p)+.04; }
 gasMat.opacity*=(1-e); gas.visible=e<.9;

 /* Chispa y luz de combustión */
 const spark=(a>=352&&a<=372)?Math.sin((a-352)/20*Math.PI):0;
 sparkSprite.material.opacity=(spark*.95+glow*.3)*(1-e);
 sparkSprite.scale.setScalar(.45+spark*.9+glow*.5);
 sparkLight.intensity=(glow*9+spark*16)*(1-e);
 sparkLight.position.y=pTop+h/2;

 return {li,le,e};
}

/* Redimensionado */
function resize(){
 const r=wrap.getBoundingClientRect();
 vw=Math.max(1,r.width); vh=Math.max(1,r.height);
 renderer.setSize(vw,vh,false); composer.setSize(vw,vh);
 camera.aspect=vw/vh; camera.updateProjectionMatrix();
 leaderSvg.setAttribute('viewBox',`0 0 ${vw} ${vh}`);
}
new ResizeObserver(resize).observe(wrap);
resize(); applyQuality();

/* Entrada cinematográfica */
camTo(V(6.8,4.9,10.2),V(0,2.4,0),1.6);
setTimeout(()=>{const h=$('#hintChip'); if(h) h.style.opacity=.45;},10000);

const clock=new THREE.Clock();
let firstFrame=true,lastSep=-1;

renderer.setAnimationLoop(()=>{
 const dt=Math.min(clock.getDelta(),.05);
 const t=clock.elapsedTime;
 const now=performance.now();

 /* Tween de ángulo (paso a paso / salto) */
 if(angleTween){
  const k=clamp((now-angleTween.start)/angleTween.dur,0,1);
  setAngle(lerp(angleTween.from,angleTween.to,easeIO(k)));
  if(k>=1){ angleTween=null; state.stepMode=false; }
 }else if(state.playing){
  setAngle(state.angle+state.rpm*6*dt);
 }

 /* Despiece + asistencia de encuadre */
 const prevE=state.explode;
 state.explode+=(state.explodeTarget-state.explode)*Math.min(1,dt*3.2);
 if(Math.abs(state.explode-state.explodeTarget)<.001) state.explode=state.explodeTarget;
 if(Math.abs(state.explode-prevE)>.0004 && !camTween){
  const ty=2.4+3.8*state.explode;
  controls.target.y+=(ty-controls.target.y)*Math.min(1,dt*3);
  const want=12.5+9*state.explode;
  tmpV.copy(camera.position).sub(controls.target);
  const d=tmpV.length(),nd=lerp(d,want,Math.min(1,dt*2.2));
  camera.position.copy(controls.target).addScaledVector(tmpV.normalize(),nd);
 }
 if(Math.abs(state.explode-lastSep)>.004){
  lastSep=state.explode;
  const pct=Math.round(state.explode*100);
  $('#sepSlider').value=pct; setRange($('#sepSlider')); $('#sepOut').textContent=pct+'%';
 }

 /* Tween de cámara */
 if(camTween){
  const k=clamp((now-camTween.start)/camTween.dur,0,1),ek=easeIO(k);
  camera.position.lerpVectors(camTween.fp,camTween.tp,ek);
  controls.target.lerpVectors(camTween.ft,camTween.tt,ek);
  if(k>=1) camTween=null;
 }
 controls.update();

 const {li,le,e}=applyKinematics(t);
 updateFlow(flowIn,dt,li/.28,e);
 updateFlow(flowEx,dt,le/.28,e);

 /* Polvo a la deriva */
 for(let i=0;i<dustCount;i++){ const s=dustSeed[i];
  dustPos[i*3]=s.x+Math.sin(t*s.v+s.s)*.6;
  dustPos[i*3+1]=s.y+Math.sin(t*s.v*.7+s.s*2)*.5;
  dustPos[i*3+2]=s.z+Math.cos(t*s.v*.5+s.s)*.6;
 }
 dustGeo.setDrawRange(0,dustCount); dustGeo.attributes.position.needsUpdate=true;

 updateHover(t);
 updateLabels();
 updateHUD();
 soundUpdate();

 if(state.quality==='baja') renderer.render(scene,camera);
 else composer.render();

 if(firstFrame){ firstFrame=false; $('#loader').classList.add('done'); }
});

syncPlayUI(); syncExplodeUI(); syncSoundUI(); updateStrokeUI(0);
} /* fin init */
</script>
</body>
</html>
```

---

## 6 · CRÉDITOS Y VERSIÓN

- **Plantilla v1.0** — "Fábrica de Simuladores 3D", derivada del simulador
  *Motor de 4 Tiempos* creado para uso en aula. Libre para compartir con compañeros
  docentes y estudiantes. Si la mejoras, sube la versión (v1.1, v1.2…) y cuenta qué cambió.
- **Tecnologías del código de muestra:** Three.js r160 (CDN), WebAudio procedural,
  HTML+CSS+JS en un solo archivo. Sin instalación, sin servidor.

**Fin del archivo. IA: ejecuta ahora la sección 3.10.**
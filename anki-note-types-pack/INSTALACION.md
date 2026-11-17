# Guía de instalación — Pack de Note Types (`Basic_Custom`, `Cloze_Custom`, `lan_1.1`, `lan_sen_1.1`)

Este paquete contiene los cuatro tipos de nota personalizados listos para importar en Anki, junto con todas sus tipografías y recursos necesarios.

> **Nota sobre nombres:** `Basic` y `Cloze` fueron exportados como `Basic_Custom` y `Cloze_Custom` para evitar conflictos con los tipos de nota nativos `Basic` y `Cloze` de Anki (de lo contrario Anki les agregaría sufijos aleatorios como `Basic-xxxx` al importar). Si deseas renombrarlos después, puedes hacerlo desde **Herramientas > Administrar tipos de nota** (*Tools > Manage Note Types*).

---

## 1. Contenido de esta carpeta

- `anki-note-types-pack.apkg`: Paquete autocontenido con el mazo `Note Types Pack (Demo)` (1 nota de ejemplo por cada tipo de nota), todas las descripciones de campo integradas y los 9 archivos multimedia requeridos empaquetados dentro.
- `skills/`: Colección de 5 skills listos para agentes de IA (Antigravity, Gemini CLI, Claude Code, Codex, OpenCode) sincronizados con estos tipos de nota:
  - `anki-card-selector`: Decide qué tipo de nota y skill usar según el contenido.
  - `anki-basic-creator`: Crea tarjetas `Basic` / `Basic_Custom` (conceptos, definiciones, hechos atómicos).
  - `anki-cloze-creator`: Crea tarjetas `Cloze` / `Cloze_Custom` (solo memorización literal: comandos, versículos, citas, sintaxis exacta).
  - `anki-lan-creator`: Crea tarjetas de vocabulario en `lan_1.1`.
  - `anki-lan-sen-creator`: Crea tarjetas contextuales de gramática/dictado en `lan_sen_1.1`.
- `fonts/`: Copia de respaldo de las 5 tipografías usadas en el CSS:
  - `_Lexend.ttf`
  - `_JetBrainsMono-Regular.ttf`
  - `_AtkinsonHyperlegibleRegular102.ttf`
  - `_SansForgetica-Regular.otf`
  - `_Dancing Script.ttf`
- `code-highlighter/`: Copia de respaldo de los 4 archivos de resaltado de sintaxis (Highlight.js + temas Solarized):
  - `_ch-pygments-solarized.css`
  - `_ch-hljs-solarized.css`
  - `_ch-highlight.js`
  - `_ch-highlight-export.js`

---

## 2. Instalación paso a paso (Anki Desktop — recomendado)

1. Abre **Anki** en tu computadora y entra al perfil donde quieras instalar los tipos de nota.
2. Haz doble clic sobre `anki-note-types-pack.apkg` (o ve a **Archivo > Importar...** / *File > Import...* y selecciona el archivo).
3. En la ventana de importación, verifica que se muestre el mazo `Note Types Pack (Demo)` y confirma la importación.
4. Al terminar, abre **Explorar** (*Browse*), selecciona el mazo `Note Types Pack (Demo)` y usa **Previsualizar** (*Preview*) en las 4 notas de ejemplo para confirmar que las fuentes y estilos cargan correctamente.
5. **Sincroniza** (*Sync*) con AnkiWeb si también estudias en **AnkiDroid** o **AnkiMobile**, para que tanto los tipos de nota como las fuentes se descarguen en tus demás dispositivos.

### Si instalas directamente en AnkiDroid / AnkiMobile

1. Abre `anki-note-types-pack.apkg` desde el gestor de archivos del teléfono y ábrelo con AnkiDroid / Anki.
2. Acepta la importación.

---

## 3. Instalación manual de recursos (solo si fallan las fuentes o el código)

Al importar el `.apkg`, Anki copia automáticamente los 9 archivos a tu carpeta `collection.media`. Si por alguna razón ves las tarjetas con fuentes genéricas o sin colores en bloques de código:

1. Localiza la carpeta `collection.media` de tu perfil:
   - **Windows:** `%APPDATA%\Anki2\<TuPerfil>\collection.media\`
   - **macOS:** `~/Library/Application Support/Anki2/<TuPerfil>/collection.media/`
   - **Linux:** `~/.local/share/Anki2/<TuPerfil>/collection.media/`
   - **Android (AnkiDroid):** `Android/data/com.ichi2.anki/files/AnkiDroid/collection.media/`
2. Copia **todos los archivos sueltos** (no las carpetas, solo los archivos) que están dentro de `fonts/` y `code-highlighter/` directamente en `collection.media\`.
3. **No elimines el guion bajo inicial (`_`)** de ningún archivo. Anki usa ese prefijo para saber que son recursos de plantilla y evitar borrarlos al ejecutar **Herramientas > Comprobar multimedia** (*Check Media*).
4. Reinicia Anki y sincroniza.

---

## 4. Limpieza opcional después de instalar

Una vez que hayas comprobado que los tipos de nota funcionan:

- Puedes **eliminar el mazo `Note Types Pack (Demo)`** (junto con sus 4 notas de ejemplo).
- **Los 4 tipos de nota (`Basic_Custom`, `Cloze_Custom`, `lan_1.1`, `lan_sen_1.1`) y los archivos de `collection.media` permanecerán instalados** en tu perfil para crear tus propias tarjetas.

---

## 5. Instalación de los Skills para Agentes de IA (`skills/`)

Cada campo dentro de los 4 tipos de nota ya incluye su **descripción humana + instrucción breve para IA** visible en el editor de campos de Anki. Además, la carpeta `skills/` incluye los 5 skills completos para que tu asistente de IA cree tarjetas respetando exactamente las plantillas y reglas pedagógicas.

Copia las 5 carpetas que están dentro de `skills/` hacia la ruta de skills de tu herramienta:

- **Antigravity:** `~/.gemini/config/skills/`
- **Gemini CLI:** `~/.gemini/skills/`
- **Claude Code:** `~/.claude/skills/`
- **Codex:** `~/.codex/skills/`
- **OpenCode:** `~/.config/opencode/skills/`

> **Tip:** Los skills detectan automáticamente mediante `anki_list_note_types` si dejaste los nombres `Basic_Custom` / `Cloze_Custom` o si los renombraste a `Basic` / `Cloze`.

---

## 6. Referencia rápida de campos y reglas de uso

### Regla clave: `Basic_Custom` vs. `Cloze_Custom`
- **`Basic_Custom`:** Úsalo para **todo conocimiento conceptual, analítico, definiciones, comparaciones, reglas situacionales o pares clave-valor**.
- **`Cloze_Custom`:** Úsalo **únicamente para memorización literal/exacta**: comandos CLI y flags, sintaxis exacta de código, versículos, citas textuales o fórmulas que deben recordarse palabra por palabra.

### `Basic_Custom` (1 tarjeta: `Card 1`)
- **Campos:** `Front`, `Back`, `Mnemonic`, `Audio`, `Mode`, `Extra`.
- **Etiqueta de tema:** Puedes iniciar `Front` con `<t>Tema | Subtema</t><br>`.
- **Nota secundaria:** En `Back`, `<br><em>nota</em>` se estiliza automáticamente como bloque aclaratorio.
- **`Mode`:** Opcional. Acepta códigos de color para el indicador circular inferior: `c`, `p`, `b`, `g`, `lg`, `y`, `o`, `r`, `gy`.
- **Código:** Soporta bloques `<pre><code class="language-python">...</code></pre>` (u otro lenguaje) usando los estilos incluidos en `code-highlighter/`.
- **Etiquetas:** La etiqueta `Obsidian_to_Anki` se oculta automáticamente en la cabecera de la tarjeta.

### `Cloze_Custom` (1 tarjeta: `Cloze`)
- **Campos:** `Text`, `Back Extra`, `Audio`, `Mode`, `Extra`.
- **`Text`:** Debe incluir al menos un hueco tipo `{{c1::texto}}` (únicamente en partes literales que debas memorizar exactas).
- **`Back Extra` vs. `Extra`:** La plantilla actual muestra **`Extra`** en el reverso (`Back Extra` no se renderiza; déjalo vacío).
- **`Mode`:** Códigos `c`, `p`, `b`, `g`, `lg`, `y`, `r`, `gy` *(en `Cloze_Custom`, `o` no tiene regla CSS propia)*.
- **Nota:** Incluye el bloque oculto del add-on *AI Explain*; si no lo tienes instalado, permanece oculto y no genera errores.

### `lan_1.1` — Vocabulario (3 tarjetas: `Reconocimiento`, `translation-to-word`, `Production`)
- **Campos:** `word`, `trans_word`, `rom`, `audio`, `image`, `menomics` *(respetar este nombre exacto)*, `definition`, `alt_trans`, `lan`, `example_1`, `example_2`, `example_3`.
- **`lan`:** Cambia el color de fondo según el idioma (`es`, `en`, `pt`, `it`, `de`). Por defecto usa el color de `en`.
- **Resaltado/Ocultamiento automático:** Escribe oraciones naturales con la palabra real (sin usar `*`). La palabra en `word` se resalta automáticamente dentro de `example_1`..`example_3` y se reemplaza por `_____` en la tarjeta `Production` (`{{type:word}}`).
- **`definition`:** Se muestra en el frente de `Production`, así que no reveles `word` dentro de la definición.
- **`alt_trans`:** Soporta enlaces con formato `etiqueta::url@etiqueta2::url2` (acepta `http://`, `https://` y `anki:`) o etiquetas simples separadas por `@`.

### `lan_sen_1.1` — Gramática y dictado (2 tarjetas: `grammar-cloze`, `cloze-dictation`)
- **Campos:** `sentence`, `target`, `pattern`, `image`, `trans_sentence`, `target_spanish`, `audio`, `audio_sen`, `other_examples`, `hint`, `explanation`, `lan`.
- **Regla obligatoria:** El texto exacto de `target` debe aparecer **una sola vez** dentro de `sentence` (sensible a mayúsculas/minúsculas; sin `*`). Si falta o aparece repetido, la tarjeta mostrará `Configuration error`.
- **`pattern`:** Describe la estructura abstracta sin incluir literalmente `target` (si lo contiene, el frente lo oculta para no revelar la respuesta).
- **`audio_sen`:** Necesario para la tarjeta `cloze-dictation` (si queda vacío mostrará `Configuration error: audio_sen is empty.`).
- **`other_examples`:** Separa múltiples ejemplos con `@` usando el `target` real (sin `*`) para renderizarlos como lista resaltada.
- **`lan`:** Acepta `es`, `en`, `pt`, `it`, `de`.

---

## 7. Sobre add-ons externos

- **No se requiere instalar ningún add-on** para usar estas plantillas.
- Los archivos `_ch-*` ya vienen incluidos para que el resaltado de sintaxis funcione tanto en escritorio como en móvil. Si deseas botones de resaltado en el editor de Anki Desktop, el bloque proviene del add-on **Anki Code Highlighter** (código `112228974`).

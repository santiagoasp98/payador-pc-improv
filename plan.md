## Plan de Correcciones Parte Central

### Categorización de las Correcciones

1.  **Nivel Crítico (Estructural):** Dividir el capítulo en dos (Diseño vs. Implementación) y reordenar las secciones. **HACER PRIMERO.**
2.  **Nivel Alto (Contenido y Claridad):** Agregar ejemplos, definir conceptos oscuros (Turno 0, RAG, Pydantic), crear anexos.
3.  **Nivel Medio (Estilo y Tono):** Eliminar lenguaje de marketing ("revolucionario"), eliminar "jerga de GitHub" ("crashes", "logs"), mejorar la redacción oral.
4.  **Nivel Bajo (Formato y Nitpicks):** Márgenes rotos por código, cursivas, negritas innecesarias, referencias cruzadas.

---

### 🗺️ El Plan de Ejecución

#### FASE 1: La Cirugía Mayor (Reestructuración)

*El tutor lo dejó claro: mezclar diseño (clases, conceptos) con implementación (código, librerías) confunde. Vamos a separar.*

1.  **Crea dos archivos nuevos (o secciones maestras en tu LaTeX):**
    *   **Nuevo Capítulo 3: Diseño y Arquitectura del Sistema.** (Aquí va el *qué* y el *por qué*).
    *   **Nuevo Capítulo 4: Implementación y Tecnologías.** (Aquí va el *cómo*, las librerías y el código).

2.  **Mueve el contenido (Copy-Paste inteligente):**
    *   **Al Cap 3 (Diseño):**
        *   Visión General (sin mencionar librerías específicas aún).
        *   **Estructura de Clases (IMPORTANTE: Mover esto al principio, antes del pipeline).** Define `World`, `Location`, `Character`, `Item`, `Puzzle`, `Objective`.
        *   El Pipeline de 5 pasos (Concepto lógico, no código Python).
    *   **Al Cap 4 (Implementación):**
        *   Integración con LLMs (Pydantic, validaciones, JSON).
        *   Ciclo de Juego (Game Loop, `game_logic.py`).
        *   Sistema RAG y Memoria (Embeddings, ChromaDB).
        *   Persistencia (MongoDB, Trazas, Turno 0).
        *   Interfaz de Usuario (Streamlit).

3.  **Escribe las nuevas introducciones:**
    *   Al inicio del Cap 3, explica que presentarás el modelo conceptual.
    *   Al inicio del Cap 4, explica que detallarás cómo se materializa ese diseño usando Python, LLMs y bases de datos.

> **Por qué hacer esto primero:** Si corriges la redacción ahora, tendrás que volver a corregirla cuando muevas el texto. Al reordenar, muchas referencias como "como veremos más adelante" cambiarán de sentido natural.

---

#### FASE 2: Rellenar los Huecos (Contenido y Ejemplos)

*El revisor pide ejemplos constantemente. El lector no está en tu cabeza.*

1.  **Enriquece la "Estructura de Clases" (Nuevo Cap 3):**
    *   **Elimina los subtítulos "cancheros"** (ej. *"Puzzle: Desafíos y Progresión"* $\rightarrow$ *"Clase Puzzle"*).
    *   **Agrega ejemplos concretos:**
        *   Para `Puzzle`: Pon una tabla con los tipos (Riddle, Logic) y un ejemplo de cada uno.
        *   Para `Objective`: Ejemplifica qué es un `SOLVE_MYSTERY` vs `GET_ITEM`.
        *   Para `AtomicMemory`: Muestra qué guarda exactamente (un JSON de ejemplo).

2.  **Clarifica el "One-Shot" y Definiciones:**
    *   Cambia el término "One-shot" por **"Generación directa"** o "Generación monolítica" (para evitar conflictos con la terminología técnica de *few-shot prompting*).
    *   **Define conceptos oscuros:**
        *   ¿Qué es el "Turno 0"? (Estado inicial para resetear).
        *   ¿Qué es "Rehidratación"? (Cargar desde BD y reconstruir objetos Python).
        *   ¿Qué es "Ruta crítica"? (Camino mínimo para ganar).
    *   Si usas términos como "Crafting" o "Alucinación", defínelos en el contexto de tu tesis o elimínalos si no son necesarios.

3.  **Crea los Anexos:**
    *   **Anexo de Prompts:** Saca todos los prompts largos del texto principal. Ponlos en un apéndice y haz referencia a ellos ("Ver Anexo A").
    *   **Anexo de MongoDB (Opcional pero recomendado):** Si la explicación de `jsonpickle` y serialización es muy densa, muévela a un anexo técnico. Deja en el capítulo solo la lógica de *por qué* lo hicieron (persistencia, replay).

---

#### FASE 3: Limpieza de Estilo (Des-marketinización)

*Tu tesis no vende un producto, presenta una investigación.*

1.  **Bajar el tono "Vendedor":**
    *   Busca palabras como: "Revolucionario", "Transforma", "Experiencia inigualable", "Evidente".
    *   Cámbialas por: "Propone", "Modifica", "Permite", "Observamos que".
    *   *Ejemplo:* En vez de "La solución evidente", usa "Basado en los experimentos, decidimos...".

2.  **Eliminar "Lenguaje de GitHub/WhatsApp":**
    *   Busca: "Crashea", "Bug", "Reintentos agotados", "Salvar mundos", "Olvidos menores", "Lo que dijo el sistema".
    *   Reemplaza por: "Fallo de ejecución", "Error", "Límite de intentos alcanzado", "Recuperar estados", "Omisiones", "La salida generada".
    *   Evita los paréntesis explicativos informales `(¡50ms típicamente!)`. Intégralos en la oración: "...con tiempos de respuesta bajos, típicamente alrededor de 50ms".

3.  **Conectores y Flujo:**
    *   Elimina los **títulos en negrita al inicio de los párrafos** (el revisor los odia). Úsalos solo si son realmente sub-secciones (`\subsubsection`). Si no, integra el tema en la primera oración del párrafo.
    *   Usa conectores: "Por otro lado", "Adicionalmente", "Como consecuencia", "Sin embargo".

---

#### FASE 4: Pulido Final (Formato)

1.  **Arreglar referencias:**
    *   Reemplaza todos los "Ver sección XX" por `\ref{sec:nombre_seccion}`.
    *   Verifica que las Figuras sean legibles. Si no, recórtalas.

2.  **Márgenes y Código:**
    *   Revisa los nombres de funciones largas (`verify_objective_completability`). En LaTeX, usa `\texttt{}` y si se sale del margen, fuerza un salto de línea o usa un entorno `sloppy` temporalmente.
    *   Asegúrate de que las palabras en inglés (si son conceptos técnicos no traducidos) estén en *cursiva* o `teletype` si son código.

3.  **Consistencia:**
    *   Decide: ¿"Ítems" u "Objetos"? (Elige una y usa "Buscar y Reemplazar").
    *   Decide: ¿"Puzzle" o "Puzle"? (Recomendación: Puzzle en cursiva o Puzle en redonda, pero consistente).


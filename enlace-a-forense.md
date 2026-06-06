# Sistema Forense de Transcripción e Indexación Masiva (e-Discovery)

**Headline:** Desarrollo de un Pipeline de Inferencia Local (On-Premise) para Auditoría Digital y Procesamiento de +15,700 Activos mediante Redes Transformer.

---

### 1. El Desafío (Contexto Legal y Técnico)
* **Problema principal:** Necesidad de procesar, auditar y clasificar más de 15,700 activos desestructurados (backups de WhatsApp, correos `.eml` y archivos multimedia) dispersos en años de comunicaciones.
* **Restricción de Soberanía (Privacidad):** Por la extrema sensibilidad de la información, se descartó el uso de IA en la nube (APIs externas) para evitar riesgos de filtración y mantener un control estricto sobre el destino de los datos probatorios.
* **Limitación de Hardware:** El procesamiento masivo de redes neuronales debía ejecutarse en hardware restringido (procesador Ryzen 7 con 8GB de RAM), obligando a optimizar la eficiencia computacional.

### 2. La Arquitectura (Data Pipeline Forense)
Diseño e implementación de un flujo de trabajo (Pipeline ETL) automatizado que orquesta distintas tecnologías para lograr la ingesta, transformación y resguardo legal de la prueba.

* **Entorno Seguro (Read-Only):** Las operaciones se realizaron exclusivamente sobre copias exactas en un entorno local aislado. Se preservaron los archivos ZIP crudos originales ("The Golden Source") para permitir eventuales extracciones manuales ante escribano público en caso de impugnaciones.
* **Data Ingestion & Limpieza:** Filtrado de ruido e irrelevancia (ej. audios de sistema) mediante scripts de Python. Para la mensajería electrónica, se extrajeron archivos `.eml` preservando los adjuntos originales y validando cabeceras mediante Outlook Desktop.
* **Transformación Acústica:** Implementación de un flujo orquestado en `PowerShell + FFmpeg` para normalizar los audios y reducir el bitrate a formato OPUS, agilizando drásticamente la velocidad de ingesta.
* **Inferencia (Faster-Whisper):** Aplicación de cuantización `int8` y multithreading, reduciendo el tiempo de procesamiento de inferencia de 3 a 1.5 minutos por activo sin degradar la precisión semántica.

### 3. Blindaje Legal y e-Discovery (Resultados)
El sistema transformó el volumen desestructurado en un "Excel Maestro" ordenado e indexado, permitiendo a un equipo legal consumir y buscar información probatoria de manera inmediata.

* **Cadena de Custodia (SHA-256):** El script generó y automatizó el hashing de cada archivo original procesado. Cada salida de datos (JSON) incluye la firma digital, vinculando de forma irrefutable la palabra escrita con el bit original.
* **Anti-Alucinación (Fidelidad Acústica):** Se configuró el parámetro `condition_on_previous_text=False` en el modelo Transformer. Esto inhabilitó el "modo autocompletar" de la IA, forzando una transcripción literal y previniendo alucinaciones para resistir auditorías de peritos de contraparte (Red Teaming).
* **Correlación Multimodal:** El índice estructurado incluyó timestamps por segmento de audio. Esto permitió cruzar el material auditivo con PDFs técnicos y capturas de pantalla de la misma marca temporal, demostrando conocimiento e intención en la causa judicial y evitando alegatos de descontextualización.

---

### 💻 Fragmento Conceptual del Pipeline de Transformación

```powershell
# Fragmento de la automatización de Transformación Acústica y Hashing
$source_dir = "C:\Evidencia_Cruda"
$export_dir = "C:\Evidencia_Procesada"

Get-ChildItem -Path $source_dir -Include *.m4a, *.mp3, *.opus -Recurse | ForEach-Object {
    $out_file = Join-Path $export_dir ($_.BaseName + "_opt.opus")
    
    # 1. FFmpeg: Normalización y compresión para optimizar ingesta del Transformer
    ffmpeg -i $_.FullName -c:a libopus -b:a 32k -v quiet $out_file
    
    # 2. Hashing SHA-256 del archivo original para asegurar la Cadena de Custodia
    $hash = (Get-FileHash $_.FullName -Algorithm SHA256).Hash
    
    # 3. Llamada a la inferencia de Whisper generando índice JSON
    whisper $out_file --model large-v2 --output_format json
}
Stack Tecnológico / Estándares:
Python (Pandas) | PowerShell | Bases de Datos Relacionales (SQLite) | Faster-Whisper (Transformers) | FFmpeg | ISO 27001 | SHA-256.

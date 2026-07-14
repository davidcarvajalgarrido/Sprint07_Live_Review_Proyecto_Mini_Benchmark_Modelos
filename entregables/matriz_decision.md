# Matriz de decisión — mini-benchmark

Rellena **una fila por pregunta** de tu `data/preguntas.json` tras ejecutar el benchmark.

| Pregunta (id) | Modelo ganador | Por qué (latencia + calidad) | Calidad 1–5 |
|---------------|----------------|------------------------------|-------------|
| pregunta_embeddings | gemini-3.1-flash-lite | Ambos excelentes (4.5/5), pero flash-lite **3.95x más rápido** (1227ms vs 4838ms). Explicación clara, estructura idéntica en calidad. | 4.5 / 4.5 |
| pregunta_vectordb | gemini-3-flash-preview | Flash-preview superior en profundidad técnica: 5 puntos clave bien desarrollados, menciona ANN/HNSW/IVF/pgvector explícitamente. Flash-lite más conciso pero válido (4.5 vs 5). Latencia: trade-off aceptable. | 5 / 4.5 |
| pregunta_tokenizacion_json | gemini-3.1-flash-lite | Ambos devuelven JSON válido. Flash-lite **3.8x más rápido** (618ms vs 2358ms). Para una tarea de formato estructurado, la velocidad es crítica sin sacrificar funcionalidad. | 4 / 4 |
| pregunta_limite_incompleta | gemini-3-flash-preview | Flash-preview detecta ambigüedad y ofrece **3 ejemplos bien documentados**. Flash-lite detecta pero ofrece solo sugerencias genéricas. Mejor manejo del caso límite. | 4 / 3.5 |
| | | | |

**Conclusión en una frase:** **gemini-3.1-flash-lite para producción** — es 3.35x más rápido con calidad comparable (4/5 promedio vs 4.375/5), ideal para un evaluador de entrevistas técnicas donde la latencia importa más que la perfección en casos complejos, salvo que necesites análisis profundos de arquitectura (usa flash-preview puntualmente).


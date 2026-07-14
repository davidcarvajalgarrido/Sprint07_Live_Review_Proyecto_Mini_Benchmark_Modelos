# Recomendación — mini-benchmark

## Caso de uso elegido

Sistema automático de evaluación de respuestas técnicas en entrevistas de ingeniería. El evaluador recibe preguntas conceptuales sobre arquitectura, optimización y principios de AI Engineering, y debe proporcionar retroalimentación precisa sobre el nivel del candidato, identificar conceptos clave y detectar casos ambiguos o incompletos.

## Modelo recomendado para producción

**gemini-3.1-flash-lite**

## Trade-off principal

**Ganas:** Latencia promedio de **1.64s vs 5.50s** con flash-preview (3.35x más rápido). En un sistema de entrevistas, esto permite procesar múltiples respuestas simultaneamente sin crear cuellos de botella, mejorando la experiencia del usuario y reduciendo costos de infraestructura.

**Pierdes:** Profundidad en análisis técnicos complejos. Flash-preview ofrece 4.5+ puntos de análisis en preguntas difíciles (e.g., RAG + Vector DBs), mientras que flash-lite es más conciso. Para preguntas conceptuales normales, ambos alcanzan 4–4.5/5, así que la pérdida es marginal.

## Riesgo o condición

**No uses flash-lite si:**
- La entrevista es **nivel senior** en arquitectura de sistemas o decisiones técnicas críticas. En ese caso, usa **flash-preview puntualmente** para preguntas donde se necesita análisis muy profundo (trade-offs, escalabilidad, alternativas).
- El candidato proporciona respuestas **incompletas o ambiguas** (como "Implementa una función en Python que..."). Flash-preview detecta mejor estos casos y ofrece ejemplos educativos; flash-lite solo pide aclaraciones genéricas.

**Valida antes de desplegar:**
1. Prueba con preguntas de nivel mid/senior de tu dominio específico y verifica que flash-lite siga dando 4/5 en comprensión técnica.
2. Monitorea la latencia en producción: si el 95º percentil supera 3s, considera un esquema híbrido (flash-lite por defecto, flash-preview para preguntas difíciles).
3. Recolecta feedback de entrevistadores: ¿perciben que el modelo se pierde en detalles arquitectónicos? Si es así, ajusta a una estrategia multi-modelo.


# AI Writing Audit

Una habilidad de Claude que audita textos en busca de patrones comunes en la escritura generada por IA, basada en la guía de detección "Signs of AI Writing" de Wikipedia.

## Qué hace esto

Esta habilidad audita sistemáticamente el texto en busca de **patrones lingüísticos y estructurales** que aparecen frecuentemente en el contenido generado por LLM, incluyendo:

- Lenguaje inflado ("stands as," "serves as," "testament to")
- Uso excesivo del léxico de la IA ("delve," "landscape," "multifaceted," "leverage")
- Estructuras formulistas (not-only-but, paralelismo de regla de tres)
- Calificadores superficiales (frases terminadas en "-ing" añadidas a los hechos)
- Indicios estructurales (uso excesivo de rayas em, encabezados en mayúsculas iniciales, negritas en línea)
- Artefactos de comunicación (referencias al corte de conocimiento, frases colaborativas)
- Problemas de citación (atribución vaga, referencias mal formadas)

La habilidad proporciona:
1. **Auditoría detallada** con patrones etiquetados y marcadores de severidad
2. **Reescritura opcional** que elimina los patrones señalados preservando el significado
3. **Registro de cambios (Changelog)** que documenta cada corrección

## Qué NO hace esto

**Esta habilidad no detecta si un texto fue escrito por una IA.**

Aquí el porqué:

- **Los humanos también escriben así.** Muchos de los patrones señalados aparecen en la escritura humana, especialmente en contextos académicos, de marketing o formales.
- **La IA puede evitar estos patrones.** Los LLM bien instruidos pueden producir texto sin ninguno de estos indicios.
- **Patrones ≠ Autoría.** Encontrar estos patrones significa que el texto tiene características comunes en la escritura de IA, nada más.

**Esta es una herramienta de auditoría de estilo, no una herramienta de detección de autoría.**

Úsela para mejorar la calidad de la escritura eliminando patrones formulistas, no para determinar si algo fue generado por IA.

## Instalación

1. Descargue `ai-writing-audit.skill` desde la [página de releases](https://github.com/a-makelky/ai-writing-audit/releases)
2. En Claude (claude.ai), vaya a la configuración de su cuenta
3. Cargue el archivo `.skill` en la sección de Skills

## Uso

### Auditoría básica

Simplemente proporcione el texto y pida a Claude que lo audite:

```
Audit this text for AI writing patterns:

[su texto aquí]
```

Claude proporcionará una auditoría detallada con patrones etiquetados como:

```
## AUDIT

1. "stands as a testament" [INFLATED] [AI-LEX +H]
2. "delve into the intricacies" [AI-LEX +H]
3. "Not only does it provide clarity, but also" [NOT-ONLY-BUT]
...

— END AUDIT: 12 issues found —
```

### Auditoría + Reescritura

Para obtener el texto corregido después de la auditoría:

```
Audit this text and provide a corrected version:

[su texto aquí]
```

Recibirá:
- Auditoría completa con problemas etiquetados
- Texto corregido con los patrones eliminados
- Registro de cambios de todas las modificaciones realizadas

## Categorías de patrones

La habilidad verifica patrones en múltiples categorías:

**Indicios de Contenido (Content Tells)**
- Lenguaje inflado y simbolismo
- Tono promocional
- Calificadores superficiales
- Secciones genéricas de perspectiva futura

**Indicios de Lenguaje (Language Tells)**
- Uso excesivo del léxico de la IA (más de 40 términos señalados)
- Estructuras formulistas
- Variación elegante
- Atribución vaga

**Indicios Estructurales (Structural Tells)**
- Patrones de formato (mayúsculas iniciales, negritas en línea)
- Uso excesivo de rayas em (em-dash)
- Artefactos de Markdown/formato

**Artefactos de Comunicación**
- Dirigirse directamente a los lectores
- Frases colaborativas ("Let me know if...")
- Referencias al corte de conocimiento (knowledge cutoff)
- Formato estilo carta

**Problemas de Citación**
- Patrones de énfasis en la fuente
- Referencias mal formadas
- Artefactos de citación (oaicite, etc.)

Consulte `references/checklist.md` para ver la lista de verificación de detección completa.

## Ejemplos

### Antes de la auditoría
```
The implementation of AI technologies stands as a testament to innovation. 
Delving into the intricate landscape of machine learning, we can see how 
these transformative tools are not only enhancing productivity, but also 
fostering unprecedented collaboration—ultimately reshaping the future of work.
```

### Después de la auditoría + reescritura
```
AI technologies show significant innovation. Machine learning tools are 
increasing productivity and enabling new forms of collaboration, changing 
how people work.
```

**Patrones eliminados:**
- "stands as a testament" → eliminada palabrería (puffery)
- "Delving into" → eliminado léxico de IA
- "intricate landscape" → simplificado
- "not only...but also" → se rompió la fórmula
- "transformative," "fostering," "unprecedented" → se reemplazó el lenguaje inflado
- Raya em (em-dash) → se reestructuró la oración
- "ultimately reshaping the future" → se eliminó la afirmación vaga

## Limitaciones

1. **Ocurren falsos positivos.** Algunos patrones señalados son perfectamente aceptables según el contexto; use su juicio.
2. **No es exhaustiva.** Los patrones evolucionan más rápido de lo que cualquier lista puede rastrear.
3. **El contexto importa.** La escritura académica, los documentos legales y los informes formales pueden utilizar legítimamente algunos de estos patrones.
4. **Las preferencias de estilo varían.** Lo que se señala como "escritura de IA" podría ser apropiado para su audiencia o dominio.

**Revise siempre los resultados de la auditoría de forma crítica.** Esta herramienta sugiere mejoras; usted decide qué mantener.

## Cuándo usar esta habilidad

✅ **Casos de uso recomendados:**
- Editar textos de marketing para ganar autenticidad
- Revisar documentación en busca de lenguaje formulista
- Mejorar la claridad de la escritura académica
- Detectar indicios de IA estilo Wikipedia antes de la publicación
- Entrenarse para reconocer estos patrones

❌ **Casos de uso NO recomendados:**
- "Probar" que el ensayo de un estudiante fue generado por IA
- Decisiones de moderación de contenido
- Sistemas automatizados de detección de IA
- Hacer acusaciones sobre la autoría

## Contribución

¿Encontró un patrón que debería añadirse? ¿Tiene sugerencias para la lista de verificación? Abra un issue o envíe un pull request.

## Créditos

Patrones de detección basados en la guía [Wikipedia: Signs of AI Writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing).

## Licencia

Licencia MIT - Consulte el archivo LICENSE para más detalles.

---

**Recuerde:** Esta herramienta identifica patrones, no autores. Úsela para mejorar la escritura, no para juzgar a los escritores.

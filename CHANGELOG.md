# CHANGELOG · claude-for-legal Argentina

> Historial de cambios del repositorio.
> Formato: fecha · archivo(s) afectado(s) · descripción del cambio · motivo.
> Las entradas más recientes van primero.
>
> Cuándo actualizar este archivo:
> - Cambio de norma listada en una sección "## Alerta normativa"
> - Modificación de un marcador o de una regla operativa
> - Agregado o eliminación de un archivo del repositorio
> - Corrección de un error normativo
> - Incorporación de un nuevo perfil de área o archivo de ejemplos
>
> Cuándo NO es necesario actualizar:
> - Correcciones tipográficas menores sin impacto en comportamiento del sistema
> - Actualizaciones de estilo sin cambio de contenido normativo

---

## Instrucción de urgencia

Cuando cambia una norma que afecta a múltiples consultas diarias (un tope indemnizatorio,
una tasa de interés, un umbral de punibilidad), actualizar primero la sección
`## Alerta normativa` del perfil afectado y registrar el cambio aquí.
No esperar a la revisión periódica.

---

## 2026

### Mayo 2026 - Limpieza final y sincronización (Etapa 4)

**Archivos modificados:**
- `argentina/fuentes.md` - agregada sección "Cómo verificar que un conector está activo" con instrucciones de verificación en Cowork y Claude Code, tabla de fallback por conector con URL y consecuencia, campo "Estado al mayo 2026" en cada entrada; marcador `[DISCREPANCIA ENTRE CONECTORES]` reemplazado por `[DISCREPANCIA ENTRE FUENTES]`
- `argentina/ejemplos-civil.md` - bloque de fórmulas genérico reemplazado por tabla por fuero (CNAC, civil y comercial federal, CABA local, PBA departamental, CNAT) con fórmula predominante, descripción técnica y ejemplo numérico; cuatro marcadores no canónicos corregidos
- `argentina/README.md` - referencia al repositorio base eliminada; estructura de archivos sincronizada con los 22 archivos reales; sección de instalación actualizada con referencias a `setup-output-TEMPLATE.md` y `diagnostico-casos-prueba.md`; tabla de perfiles con columna "Complementos"; referencias a "plugins" corregidas

**Normas afectadas:** ninguna. Los cambios son de estructura y documentación.

---

### Mayo 2026 - Gaps de cobertura (Etapa 3)

**Archivos nuevos:**
- `argentina/contratos-CLAUDE.md` - perfil unificado para revisión y redacción de contratos bajo derecho argentino; cubre flujo de revisión (clasificación + red-flags + análisis por tipo), flujo de redacción con preguntas de diagnóstico previo, y 7 tipos contractuales con lógica específica (servicios profesionales, SaaS, compraventa, locación, NDA, mutuo, agencia/concesión/franquicia)
- `argentina/diagnostico-casos-prueba.md` - tres casos ficticios con diagnóstico esperado completo para verificar el skill: demanda laboral por despido (9 marcadores esperados), demanda civil por mala praxis (14 marcadores), revisión de cláusulas de pacto de accionistas (10 marcadores)

**Normas afectadas:** ninguna. Los archivos nuevos aplican normativa ya incluida en los perfiles de área.

---

### Mayo 2026 - Integración interna (Etapa 2)

**Archivos modificados:**
- `argentina/CLAUDE.md` - agregados bloques "Protocolo ante alucinación normativa" y "Routing hacia perfiles de área"; estructura del repo actualizada con archivos nuevos de Etapa 1
- `argentina/civil-CLAUDE.md` - agregado bloque "Archivos complementarios"; marcadores `[VACÍO CUANTIFICATIVO]` y `[VERIFICAR CRITERIO DE LA SALA]` reemplazados por formas canónicas; fecha de verificación en alertas normativas
- `argentina/societario-CLAUDE.md` - agregado bloque "Archivos complementarios"; marcadores `[VERIFICAR RESOLUCIÓN IGJ/DPPJ VIGENTE]`, `[VACÍO DOCUMENTAL]` y `[VERIFICAR UMBRAL CNDC VIGENTE]` reemplazados; fecha de verificación en alertas normativas
- `argentina/laboral-CLAUDE.md` - agregado bloque "Archivos complementarios"; fecha de verificación en alerta DNU
- `argentina/administrativo-CLAUDE.md`, `argentina/tributario-CLAUDE.md`, `argentina/penal-CLAUDE.md`, `argentina/familia-CLAUDE.md`, `argentina/concursos-CLAUDE.md` - fecha de verificación agregada en cada sección "## Alerta normativa"

**Normas afectadas:** ninguna. Los cambios son de estructura, marcadores y referencias cruzadas.

---

### Mayo 2026 - Reorganización y estandarización inicial (Etapa 1)

**Archivos nuevos:**
- `argentina/marcadores-GLOSARIO.md` - glosario canónico con 15 formas canónicas en 4 categorías; tabla de equivalencias que mapea los 40+ marcadores anteriores a su forma canónica
- `argentina/setup-output-TEMPLATE.md` - template con variables mapeadas a cada pregunta de la entrevista, instrucciones de generación para el sistema, y ejemplo de output completo
- `argentina/CHANGELOG.md` - este archivo; incluye tabla de normas de alta volatilidad con fecha de última verificación

**Archivos modificados:**
- `argentina/setup-interview.md` - agregada referencia a `setup-output-TEMPLATE.md` en el flujo de output
- `argentina/CLAUDE.md` - agregada referencia al glosario de marcadores

**Motivo:** estandarización de marcadores (existían más de 40 variantes equivalentes distribuidas entre archivos); formalización del output de la entrevista; trazabilidad de cambios normativos.

**Normas afectadas:** ninguna. Los cambios son de forma, no de contenido normativo.

---

## Plantilla de entrada

Copiar y completar para cada cambio:

```
### [Mes Año]

**Archivos afectados:**
- `ruta/archivo.md` - sección afectada

**Cambio:**
[descripción del cambio]

**Motivo:**
[norma modificada / error detectado / nueva funcionalidad]

**Normas vigentes actualizadas:**
- [norma]: [cambio concreto]

**Impacto en marcadores:**
- [marcador afectado]: [cambio en comportamiento]

**Fuente:**
- [URL o referencia de la norma que motivó el cambio]
```

---

## Normas de alta volatilidad · estado al momento de la última revisión

Esta tabla recoge las normas con mayor frecuencia de cambio. Verificar antes de aconsejar.
Actualizar la columna "Última verificación" cuando se confirme la vigencia.

| Norma | Área | Dato volátil | Última verificación |
|---|---|---|---|
| Art. 245 LCT - tope indemnizatorio | Laboral | Monto del tope por CCT | Mayo 2026 - verificar por CCT |
| Acta CNAT - tasa de interés | Laboral | Tasa y fecha de vigencia | Mayo 2026 - verificar acta vigente |
| Resolución SRT - prestaciones LRT | Laboral / LRT | Montos de prestaciones | Mayo 2026 - verificar RG vigente |
| DNU 70/2023 - modificaciones LCT | Laboral | Estado judicial de cada modificación | Mayo 2026 - algunas suspendidas, verificar |
| Ley 27.430 art. 1 - umbral penal tributario | Tributario | Monto de punibilidad | Mayo 2026 - verificar si fue actualizado |
| Monto mínimo recurso TFN | Tributario | Monto habilitante | Mayo 2026 - verificar norma vigente |
| Capital mínimo IGJ/DPPJ | Societario | Monto actualizado por resolución | Mayo 2026 - verificar resolución vigente |
| Sindicatura obligatoria SA - parámetros | Societario | Parámetros de activación | Mayo 2026 - verificar resolución IGJ/DPPJ |
| Régimen cambiario BCRA | Contratos / M&A | Restricciones al giro de divisas | Mayo 2026 - verificar comunicaciones BCRA |
| Ley 27.551 - locaciones urbanas | Familia / Civil | Modalidad de actualización del alquiler | Mayo 2026 - verificar estado de modificaciones |
| Tasas de interés fueros civiles y comerciales | Civil / Comercial | Tasa activa BNA, variantes por sala | Mayo 2026 - verificar actas CNAC / CNACOM |
| Prestaciones alimentarias - fórmulas | Familia | Criterio por fuero | Mayo 2026 - verificar criterio sala actuante |

---

*Última actualización: mayo 2026*
*Autor: Dr. Cristian Aboitiz · [@abogadoaboitiz](https://x.com/abogadoaboitiz)*

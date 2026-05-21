# Confidencialidad y seguridad

Este repositorio contiene configuración para el procesamiento de material jurídico
con modelos de lenguaje. El uso profesional responsable requiere observar las
obligaciones del secreto profesional (art. 10 Ley 23.187; normas colegiales
equivalentes) y la Ley 25.326 de Protección de Datos Personales.

---

## Egreso de datos

Claude Code, Claude.ai Projects y cualquier cliente que use la API de Anthropic
envían el contenido del contexto a los servidores de Anthropic para su
procesamiento. Esto aplica aunque el cliente corra localmente en tu máquina.
No existe aislamiento absoluto de los datos por el solo hecho de usar una
aplicación de escritorio o terminal.

Consecuencia práctica: todo material que ingrese al contexto de una sesión
debe estar previamente anonimizado. No hay excepción.

Política de datos de Anthropic: https://www.anthropic.com/legal/privacy

---

## Protocolo de anonimización

Antes de pegar cualquier pieza procesal, contrato, dictamen o documento con
datos de partes reales, reemplazá los siguientes elementos por marcadores
genéricos:

| Dato real | Marcador sugerido |
|---|---|
| Nombre de imputado / acusado | `[IMPUTADO_1]`, `[IMPUTADO_2]` |
| Nombre de víctima / damnificado | `[VICTIMA_1]`, `[VICTIMA_2]` |
| Nombre de testigo | `[TESTIGO_1]`, `[TESTIGO_2]` |
| Nombre de cliente (cualquier fuero) | `[CLIENTE]` |
| Nombre de contraparte | `[CONTRAPARTE]` |
| Número de expediente / causa | `[NRO_CAUSA]` |
| CUIT / CUIL / DNI | `[CUIT]`, `[CUIL]`, `[DNI]` |
| Domicilio real | `[DOMICILIO]` |
| Número de cuenta bancaria | `[CUENTA]` |
| Datos de fiscalía o juzgado interviniente | `[ORGANO_JURISDICCIONAL]` |
| Fechas que permitan identificar la causa | `[FECHA]` (si son determinantes) |

El sistema trabaja igual con datos anonimizados. La precisión del análisis
jurídico no depende de los nombres reales.

---

## Qué no meter nunca en contexto

Con independencia de la anonimización, hay categorías de información que
no deben ingresarse bajo ninguna circunstancia:

- Imágenes o descripciones de material de abuso sexual infantil (MASI),
  aunque sea en el marco de una causa penal en la que intervenís como defensor
  o querellante.
- Información clasificada o reservada por decisión judicial (art. 204 CPPN
  y equivalentes provinciales).
- Datos biométricos de personas físicas.
- Contenido de escuchas telefónicas o interceptaciones en estado de reserva
  sumarial.
- Acuerdos de colaboración eficaz (Ley 27.304) antes de su homologación.
- Información cubierta por acuerdo de confidencialidad con terceros que
  no contempla el procesamiento por IA.

---

## Materia penal: consideraciones específicas

El secreto profesional del defensor penal tiene rango constitucional (art. 18
CN) y no admite excepciones. Antes de usar cualquier herramienta de este
repositorio con material de una causa penal activa:

1. Anonimizá según el protocolo anterior.
2. Evaluá si la información a ingresar es determinante para identificar
   la causa o las partes aun sin nombres explícitos (número de causa,
   fecha y tribunal combinados pueden ser suficientes para identificación).
3. No uses el sistema para analizar material probatorio original; usalo
   para trabajar sobre el escrito o estrategia que vas a generar vos.

---

## Reporte de problemas de seguridad

Si encontrás una vulnerabilidad en la configuración del sistema que pueda
comprometer datos de usuarios del repositorio, reportala por mensaje directo
a [@abogadoaboitiz](https://x.com/abogadoaboitiz) antes de publicarla.

---

*Última actualización: mayo 2026*

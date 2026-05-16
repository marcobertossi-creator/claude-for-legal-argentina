# Fuentes normativas argentinas · Conectores MCP

Repositorios de la comunidad que conectan claude-for-legal directamente
con las fuentes oficiales argentinas. Reemplazan los conectores originales
del repositorio base (Westlaw, CourtListener, Everlaw) para práctica local.

Los conectores son la segunda capa del sistema. Los plugins funcionan
sin ellos usando el perfil de práctica como única configuración.
Con los conectores, el sistema consulta fuentes primarias automáticamente
sin que el abogado tenga que pegar el texto de la norma en la sesión.

---

## Conectores disponibles

### 1. Ansvar-Systems/argentine-law-mcp

**Repositorio:** https://github.com/Ansvar-Systems/argentine-law-mcp
**Fuentes:** InfoLEG · SAIJ
**Función:** Devuelve el texto literal de normas nacionales argentinas sin
pasar por ningún modelo de lenguaje. Consulta directa a InfoLEG.

Casos de uso:
- Verificar el texto actual de un artículo del CCCN, LCT, LDC u otra norma nacional
- Confirmar si una norma fue modificada o derogada
- Obtener el texto de una ley especial sin buscarlo manualmente

Limitaciones:
- Solo normas nacionales (no provinciales)
- No incluye jurisprudencia
- No realiza análisis: devuelve texto literal

---

### 2. Psflores/Legal-MCP-Server-

**Repositorio:** https://github.com/Psflores/Legal-MCP-Server-
**Fuentes:** Poder Judicial de la Nación · Justicia CABA
**Función:** Búsqueda de jurisprudencia de fueros nacionales y CABA.

Casos de uso:
- Buscar fallos por doctrina antes de citar en un escrito
- Verificar criterio de la sala en una materia específica
- Rastrear evolución jurisprudencial sobre un instituto

Limitaciones:
- No cubre PBA (SCBA ni cámaras de apelación provinciales)
- Los resultados deben verificarse antes de citar: el conector busca,
  no garantiza que el fallo sea el más reciente o representativo

---

### 3. guidobonomini/argentina-law-mcp-server

**Repositorio:** https://github.com/guidobonomini/argentina-law-mcp-server
**Función:** Análisis semántico de documentos legales, glosario judicial
argentino, detección de riesgos calibrada para praxis local.

Casos de uso:
- Análisis de contratos con terminología jurídica argentina nativa
- Corrección de terminología cuando el sistema genera términos de common law
- Consistencia terminológica en documentos largos

Limitaciones:
- No conecta a fuentes primarias oficiales
- El análisis semántico está basado en praxis documentada, no en texto oficial
- Complementa al conector 1, no lo reemplaza

---

### 4. datos-justicia-argentina/Tesauro-Saij-de-Derecho-Argentino

**Repositorio:** https://github.com/datos-justicia-argentina/Tesauro-Saij-de-Derecho-Argentino
**Fuente:** SAIJ
**Función:** Vocabulario controlado para búsqueda jurídica. Mapea sinónimos,
términos preferidos y jerarquías conceptuales del derecho argentino.

Casos de uso:
- Mejorar la precisión de búsquedas jurisprudenciales
- Evitar que el sistema use términos de common law cuando existe equivalente argentino
- Consistencia terminológica en documentos largos

Limitaciones:
- Es un vocabulario de referencia, no un conector a fuentes primarias
- No devuelve texto normativo ni fallos: solo estructura conceptual

---

### 5. SCBA - Jurisprudencia PBA

**Estado:** conector no disponible actualmente en la comunidad. Ver fuentes directas abajo.

La Suprema Corte de Justicia de la Provincia de Buenos Aires (SCBA) tiene
jurisprudencia relevante especialmente en materia laboral, civil y administrativo
provincial que no está cubierta por ninguno de los conectores anteriores.

**Alternativa mientras no hay conector MCP:**
Acceder directamente a https://scba.gov.ar/jurisprudencia/ y pegar el texto
del fallo en la sesión para que el sistema lo procese. Indicar siempre:
sala, fecha, carátula y número de expediente.

**Para quien quiera desarrollar el conector:**
La SCBA tiene una API de consulta pública. La contribución de un conector MCP
que apunte a esa API sería la de mayor impacto para práctica bonaerense.

---

## Tabla de decisión - qué conector usar

| Necesidad | Conector recomendado | Alternativa |
|---|---|---|
| Verificar texto de una norma nacional | 1 (Ansvar) | InfoLEG directo |
| Buscar jurisprudencia CABA / fueros nacionales | 2 (Psflores) | PJN directo |
| Buscar jurisprudencia PBA | Sin conector | SCBA directo |
| Análisis semántico / terminología | 3 (guidobonomini) | - |
| Mejorar búsquedas jurisprudenciales | 4 (Tesauro SAIJ) | SAIJ directo |

**¿Son acumulables?**

Sí, pero con criterio. Las combinaciones útiles son:

- **1 + 2:** para trabajo donde se necesita tanto el texto de la norma como
  jurisprudencia que la interpreta. El flujo recomendado es: primero verificar
  el texto con 1, luego buscar jurisprudencia con 2 usando la terminología
  correcta del texto oficial.

- **4 + 2:** el Tesauro (4) mejora la calidad de las búsquedas de jurisprudencia (2).
  Activar el 4 para normalizar los términos antes de la búsqueda.

- **1 + 3:** el 3 analiza el contrato con glosario argentino; el 1 verifica
  las normas que el 3 cita. El 3 no reemplaza al 1 porque no accede a texto oficial.

**¿Qué pasa si dos conectores dan resultados contradictorios?**

Los conectores 1 y 2 acceden a fuentes primarias oficiales: en caso de contradicción
con cualquier otro conector o con el conocimiento base del sistema, prevalece
la fuente primaria. Los conectores 3 y 4 son instrumentos auxiliares:
si contradicen una fuente primaria, reportar la discrepancia al abogado
con el marcador:

```
[DISCREPANCIA ENTRE CONECTORES: el conector [X] indica [A] / la fuente primaria
 indica [B]. Verificar directamente en [fuente primaria] antes de proceder.]
```

---

## Fuentes primarias oficiales (sin conector MCP)

Estas fuentes no tienen conector MCP disponible actualmente. Acceso directo
por el abogado para verificación manual. Son la fuente de verdad cuando
hay discrepancia con cualquier conector.

| Fuente | URL | Uso principal |
|---|---|---|
| InfoLEG | infoleg.gob.ar | Texto oficial de normas nacionales |
| SAIJ | saij.gob.ar | Jurisprudencia, doctrina, legislación provincial |
| PJN | pjn.gov.ar | Acordadas y jurisprudencia federal |
| SCBA | scba.gov.ar | Jurisprudencia PBA - fuente primaria bonaerense |
| Poder Judicial CABA | buenosaires.gob.ar/jusbaires | Jurisprudencia fuero local CABA |
| AAIP | argentina.gob.ar/aaip | Disposiciones de datos personales |
| IGJ | igj.gob.ar | Resoluciones societarias CABA |
| DPPJ | gba.gob.ar/dppj | Resoluciones societarias PBA |
| CNV | cnv.gov.ar | Normas y resoluciones mercado de capitales |
| BCRA | bcra.gov.ar | Normativa cambiaria y financiera |
| COMARB | comarb.gov.ar | Convenio Multilateral - Ingresos Brutos |
| TFN | tfnacional.gov.ar | Jurisprudencia tributaria |

---

## Instalación de conectores MCP

**En Claude Cowork (aplicación de escritorio):**
1. Abrir Claude Cowork
2. Ir a Configuración > MCP Servers
3. Agregar la URL del repositorio del conector
4. Verificar que el conector aparezca activo antes de usarlo

**En Claude Code:**
Agregar la URL del conector al archivo `.mcp.json` del plugin.
Ver instrucciones detalladas en el README del repositorio de cada conector.

Para instrucciones específicas de cada conector, consultar el README
del repositorio correspondiente. Los conectores son proyectos de la comunidad:
si encontrás un error o un conector que dejó de funcionar, reportarlo
en el issue tracker del repositorio correspondiente.

---

## Contribuciones

Si desarrollás un conector para una fuente no cubierta, especialmente SCBA
o jurisprudencia provincial de otras provincias, abrí un PR en este repositorio
para agregar la referencia a esta lista.

---

*Última actualización: mayo 2026*
*Autor: Dr. Cristian Aboitiz · [@abogadoaboitiz](https://x.com/abogadoaboitiz)*

# claude-for-legal · Adaptación Argentina

Fork de [anthropics/claude-for-legal](https://github.com/anthropics/claude-for-legal) configurado para práctica legal argentina.

El repositorio original cubre 12 plugins y más de 80 agentes. Está construido íntegramente sobre derecho norteamericano: Delaware, Nueva York, common law, at-will employment, GDPR. Este fork agrega una capa de configuración argentina sin modificar los plugins originales.

---

## Estructura

```
argentina/
  CLAUDE.md                   # Perfil de práctica general (reemplaza al original)
  administrativo-CLAUDE.md    # Perfil para derecho administrativo
  civil-CLAUDE.md             # Perfil para derecho civil (CCCN)
  concursos-CLAUDE.md         # Perfil para concursos y quiebras (LCQ)
  ejemplos-laboral.md         # Casos de liquidación resueltos con checklist de rubros
  familia-CLAUDE.md           # Perfil para derecho de familia
  laboral-CLAUDE.md           # Perfil para derecho del trabajo (LCT)
  penal-CLAUDE.md             # Perfil para derecho penal
  societario-CLAUDE.md        # Perfil para derecho societario (LGS)
  tributario-CLAUDE.md        # Perfil para derecho tributario
  red-flags-contratos.md      # Lista de alertas para revisión de contratos
  fuentes.md                  # Conectores a bases de datos normativas locales
```

Los plugins originales quedan intactos. Todo el material argentino vive en la carpeta `argentina/`.

---

## Qué hace este fork

**Configura el sistema para operar bajo:**
- CCCN (Ley 26.994) para contratos y obligaciones
- LCT (Ley 20.744) y modificatorias para materia laboral
- Ley 25.326 y disposiciones AAIP para privacidad y datos personales
- CPCCN para fueros nacionales y federales / CPCCBA para PBA
- LDC (Ley 24.240) para contratos de consumo
- LGS para societario

**Reemplaza la lógica de common law en tres plugins críticos:**
- `commercial-legal` - análisis de contratos bajo CCCN, no bajo consideration/indemnification caps
- `employment-legal` - modelo de despido con indemnización obligatoria (art. 245 LCT), no at-will
- `privacy-legal` - habeas data bajo Ley 25.326, no GDPR/DSAR

**Agrega red flags específicas del derecho argentino** para revisión automática de contratos.

---

## Antes de empezar

Necesitás:
- Cuenta de Claude.ai con plan Pro
- Claude Cowork (aplicación de escritorio, descargable desde claude.ai)
- Cuenta de GitHub gratuita

No necesitás saber programar para la configuración base. Para conectar fuentes normativas locales (fase 2), vas a necesitar ayuda técnica.

---

## Instalación

### Paso 1: Fork

Hacé click en "Fork" arriba a la derecha. Eso crea una copia en tu cuenta. No descargues el ZIP: el fork te permite incorporar actualizaciones del repositorio original sin pisar tu configuración local.

### Paso 2: Perfil de práctica general

Abrí `argentina/CLAUDE.md` y cargá su contenido en las instrucciones del Project de Claude que vas a usar para práctica general. Completá la sección "Documentos semilla de la firma" con tus propios documentos de referencia: contratos tipo, escritos representativos, modelos internos. Es la sección de mayor impacto práctico en la calidad del output.

### Paso 3: Perfiles por área

Para cada área de práctica que uses, abrí el archivo correspondiente y completá las variables de la sección "Configuración inicial" al inicio del archivo. Cada variable tiene un ejemplo concreto. Las variables mínimas son fuero habitual y rol predominante; sin ellas el sistema opera con supuestos genéricos.

Los perfiles disponibles:

| Archivo | Área | Variable crítica |
|---|---|---|
| `laboral-CLAUDE.md` + `ejemplos-laboral.md` | Derecho del trabajo (LCT) | CCT_HABITUAL para el tope art. 245 |
| `administrativo-CLAUDE.md` | Derecho administrativo | FUERO_HABITUAL para los plazos procesales |
| `civil-CLAUDE.md` | Derecho civil (CCCN) | AREAS_PRACTICA |
| `penal-CLAUDE.md` | Derecho penal | ESPECIALIDADES |
| `familia-CLAUDE.md` | Derecho de familia | AREAS_PRACTICA |
| `societario-CLAUDE.md` | Societario y M&A | JURISDICCION_INSCRIPCION (IGJ / DPPJ) |
| `tributario-CLAUDE.md` | Derecho tributario | TRIBUTOS_FRECUENTES |
| `concursos-CLAUDE.md` | Concursos y quiebras (LCQ) | ROL_PREDOMINANTE |

Cargá el perfil del área junto con el `CLAUDE.md` general en las instrucciones del Project correspondiente.

### Paso 4: Plugins críticos

Para los tres plugins del repo original que requieren reescritura completa de lógica, el `CLAUDE.md` argentino incluye instrucciones específicas por sección. Ver el archivo para el detalle.

---

## Fuentes normativas (fase 2)

Conectores de la comunidad que apuntan directamente a las fuentes oficiales argentinas:

| Repositorio | Fuente | Función |
|---|---|---|
| [Ansvar-Systems/argentine-law-mcp](https://github.com/Ansvar-Systems/argentine-law-mcp) | InfoLEG / SAIJ | Texto literal de normas nacionales |
| [Psflores/Legal-MCP-Server-](https://github.com/Psflores/Legal-MCP-Server-) | PJN / CABA | Jurisprudencia fueros nacionales |
| [guidobonomini/argentina-law-mcp-server](https://github.com/guidobonomini/argentina-law-mcp-server) | Praxis local | Análisis semántico, glosario judicial |
| [datos-justicia-argentina/Tesauro-Saij](https://github.com/datos-justicia-argentina/Tesauro-Saij-de-Derecho-Argentino) | SAIJ | Vocabulario controlado para búsqueda jurídica |

No son necesarios para empezar. Los plugins funcionan con el perfil de práctica como única configuración. Los conectores son la segunda capa: permiten que el sistema consulte InfoLEG automáticamente antes de analizar una norma.

---

## Lo que podés hacer desde el día uno

**Contratos:**
- Revisar contratos contra la lista de red flags argentina, con referencia a norma aplicable (CCCN, LCT, LDC)
- Redactar borradores de contratos tipo (NDA, prestación de servicios, compraventa) con CCCN como base
- Detectar cláusulas abusivas en contratos de adhesión y consumo

**Societario y M&A:**
- Preparar briefings de due diligence con checklist adaptado a LGS y normativa IGJ/DPPJ
- Armar pactos de accionistas con análisis de ejecutabilidad en Argentina
- Verificar requisitos de notificación a la CNDC en operaciones de concentración

**Laboral:**
- Calcular liquidaciones finales (art. 245 LCT + agravantes Ley 24.013 / Ley 25.323 / art. 80)
- Analizar estrategia desde el trabajador o el empleador con carga probatoria invertida
- Redactar telegramas y cartas documento laborales

**Administrativo:**
- Verificar agotamiento de la vía administrativa y plazos de caducidad (art. 25 LNPA)
- Analizar recursos administrativos y acciones contenciosas en los tres fueros (federal, CABA, PBA)

**Penal:**
- Analizar estrategia de defensa por etapa procesal y código aplicable (CPPN / CPPF / CPPCABA / CPPBA)
- Evaluar procedencia de colaboración eficaz (Ley 27.304) y proceso de flagrancia (Ley 27.272)

**Familia:**
- Armar convenios reguladores de divorcio con todos los institutos del CCCN
- Analizar alimentos, cuidado personal y régimen comunicacional con jurisprudencia del fuero

**Tributario:**
- Analizar recursos ante el TFN y la CNACAF
- Revisar compliance bajo Ley 25.326 (habeas data) con vocabulario argentino nativo

**Concursal:**
- Verificar privilegios de créditos y estrategia de verificación
- Analizar acciones de recomposición patrimonial (período de sospecha, arts. 118-119 LCQ)

---

## Lo que no reemplaza

El criterio del abogado. La responsabilidad profesional. La firma.

Todo output del sistema es un borrador. No sabe qué pasó en la negociación, no conoce la relación con la contraparte, no tiene el expediente completo. Acelera la parte mecánica. Las decisiones son siempre del abogado.

---

## Contribuciones

Este repositorio es una vitrina de referencia, no un proyecto con mantenimiento activo. Si encontrás un error normativo, abrí un issue con la norma correcta y la fuente. Si querés adaptar el perfil para otra jurisdicción (Uruguay, Chile, Colombia), forkéalo y avisame.

---

## Autor

Dr. Cristian Aboitiz · [@abogadoaboitiz](https://x.com/abogadoaboitiz)  
Abogado (CPACF) · CABA y GBA · Legal tech & IA aplicada a práctica jurídica argentina

*Última actualización: mayo 2026*

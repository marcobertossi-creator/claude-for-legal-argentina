# Perfil de práctica · Contratos bajo derecho argentino

> Archivo de configuración para el sistema claude-for-legal.
> Complementa el perfil general (argentina/CLAUDE.md) con lógica específica
> para revisión y redacción de contratos bajo derecho argentino.
> Este perfil es transversal: aplica en práctica civil, comercial, societaria
> y laboral cuando la tarea principal es un contrato.
>
> Cargar junto con:
> - `argentina/CLAUDE.md` (base obligatoria)
> - `argentina/red-flags-contratos.md` (lista de alertas - el sistema la aplica automáticamente)
> - El perfil de área específico cuando el contrato involucra una rama especializada
>   (laboral, societario, tributario, etc.)
>
> **Configuración inicial:** no requiere variables obligatorias. El sistema
> identifica el tipo de contrato y el régimen aplicable al inicio de cada sesión.

---

## Alerta normativa - normas de vigencia variable

*Última verificación de esta sección: mayo 2026. Actualizar cuando cambie alguna de las normas listadas.*

### Régimen de locaciones urbanas
La Ley 27.551 y sus modificatorias (Ley 27.737, DNU 70/2023) cambiaron
en varias oportunidades los plazos mínimos, el mecanismo de actualización
del precio y las garantías admisibles. Ante cualquier contrato de locación urbana:
```
[VERIFICAR VIGENCIA: Ley 27.551 y modificatorias - régimen aplicable al momento
 del contrato y al momento de la consulta pueden diferir]
```

### Régimen cambiario
Las restricciones al giro de divisas y el tipo de cambio aplicable a contratos
con precio en moneda extranjera se modifican por normativa del BCRA con frecuencia.
```
[VERIFICAR RÉGIMEN CAMBIARIO VIGENTE: normativa BCRA - verificar antes de
 aconsejar sobre cualquier obligación en moneda extranjera]
```

### Derecho intertemporal
Contratos celebrados antes del 1° de agosto de 2015 se rigen por el CC (Ley 340)
y el CCom (Ley 2637), salvo disposición transitoria específica del CCCN (art. 7).
Contratos en curso de ejecución: el CCCN aplica a las consecuencias no consumadas.
```
[VERIFICAR RÉGIMEN APLICABLE: contrato anterior al CCCN - determinar si aplica
 CC/CCom o CCCN según fecha de celebración y consecuencia analizada]
```

---

## Flujo de trabajo para revisión de contrato aportado

### Paso 1 - Clasificación inicial (siempre, antes de cualquier análisis)

El sistema responde estas cuatro preguntas antes de abrir el contrato:

**1a. ¿Es de adhesión o paritario?**
- Adhesión (arts. 984-989 CCCN [VERIFICAR VIGENCIA]): una parte predispone las condiciones; la otra solo puede aceptar o rechazar. Aplica control de cláusulas abusivas con estándar más severo.
- Paritario: las partes negociaron las condiciones. El control de abusividad es más acotado.
- Señales de adhesión: formulario impreso, términos y condiciones, contrato de plataforma digital, póliza de seguro, mutuo bancario.

**1b. ¿Hay consumidor?**
- Consumidor presente (arts. 1092-1122 CCCN / LDC [VERIFICAR VIGENCIA]): activa el estatuto del consumidor. Las consecuencias van más allá de la nulidad de cláusulas: afectan la interpretación de todo el contrato, la distribución de cargas y el foro competente.
- Indicios de relación de consumo: una parte es persona humana o jurídica que adquiere un bien o servicio para uso final; la otra parte es proveedor en el marco de su actividad empresarial.

**1c. ¿Hay relación laboral encubierta?**
- Verificar si el contrato de locación de servicios, agencia, franquicia o similar encubre una relación de dependencia (arts. 22-23 LCT [VERIFICAR VIGENCIA post-DNU 70/2023]).
- Señales: exclusividad, horario fijo, uso de elementos del comitente, subordinación jurídica y económica, facturación como único ingreso del prestador.
- Si hay presunción de relación laboral: alertar y activar perfil laboral antes de continuar.

**1d. ¿El contrato involucra derecho extranjero?**
- Si hay cláusula de ley aplicable extranjera o prórroga de jurisdicción al extranjero: activar análisis DIPr (arts. 2594-2671 CCCN [VERIFICAR VIGENCIA]) antes de evaluar la validez de las cláusulas.
- En contratos de consumo: la prórroga de jurisdicción al extranjero es inválida (art. 2654 CCCN [VERIFICAR VIGENCIA]) — red flag de nulidad absoluta.

---

### Paso 2 - Red-flags (siempre, en el orden del archivo `red-flags-contratos.md`)

El sistema aplica la lista completa de red-flags del archivo `argentina/red-flags-contratos.md`.
No omitir ninguna categoría. No detener el análisis al encontrar la primera red-flag.

Marcadores canónicos según `argentina/marcadores-GLOSARIO.md`:
- `[RED FLAG - NULIDAD ABSOLUTA: descripción - norma: norma aplicable [VERIFICAR VIGENCIA]]`
- `[RED FLAG - RIESGO ALTO: descripción - observación: descripción del problema]`
- `[RED FLAG - RIESGO MEDIO: descripción]`

---

### Paso 3 - Análisis por tipo de contrato

Después de las red-flags, el sistema aplica la lógica específica del tipo contractual.
Ver sección "Tipología de contratos" más abajo.

---

### Paso 4 - Informe de revisión

```
## Informe de revisión · [tipo de contrato] · [fecha]

### Clasificación
- Tipo: adhesión / paritario / mixto
- Consumidor presente: sí / no / a verificar
- Relación laboral encubierta: sí / no / a verificar
- Derecho extranjero involucrado: sí / no

### Red-flags de nulidad absoluta
[Ninguna detectada]
[o desarrollo por ítem con cláusula textual o paráfrasis + norma + consecuencia]

### Red-flags de riesgo alto
[Ninguna detectada]
[o desarrollo por ítem con propuesta de redacción alternativa]

### Red-flags de riesgo medio
[Ninguna detectada / listado con nota breve por ítem]

### Análisis específico por tipo
[Observaciones propias del tipo contractual no cubiertas por las red-flags]

### Normas con verificación pendiente
[Listado: norma - motivo]

### Estado del análisis
Marcadores pendientes: [dato concreto que falta para resolverlos]
Decisiones estructurales por defecto: [o "Ninguna"]
```

Si el contrato fue aportado con instrucción de modificación directa: entregar
el informe primero y preguntar si proceder. No modificar antes de que el abogado
lea el informe. Esta regla no puede ser suspendida por instrucción del usuario.

---

## Flujo de trabajo para redacción de contrato nuevo

### Preguntas de diagnóstico previo (hacer antes de redactar)

1. ¿Qué tipo de contrato es? (ver tipología abajo)
2. ¿Quiénes son las partes? ¿Personas humanas o jurídicas? ¿Nacionales o extranjeras?
3. ¿Hay consumidor? ¿Hay relación laboral encubierta probable?
4. ¿El contrato es de adhesión o se negociará?
5. ¿Cuál es el objeto exacto? ¿Obligación de medios o de resultado (art. 774 CCCN [VERIFICAR VIGENCIA])?
6. ¿Hay precio? ¿En qué moneda? ¿Hay mecanismo de actualización?
7. ¿Cuál es el plazo? ¿Es de tracto sucesivo?
8. ¿Hay garantías? ¿Cuáles?
9. ¿Se prevé prórroga, rescisión anticipada o resolución? ¿Con qué requisitos?
10. ¿Hay confidencialidad? ¿Con qué alcance y plazo?
11. ¿Hay cláusula penal? ¿El monto es razonable (art. 794 CCCN [VERIFICAR VIGENCIA])?
12. ¿Qué foro y ley aplicable se pretende?

Si el abogado no respondió alguna de estas preguntas antes de pedir la redacción,
el sistema pregunta las que impactan en la estructura del contrato (1-5) y redacta
con marcadores para las restantes.

### Estructura estándar de un contrato

```
1. Encabezado
   - Lugar y fecha
   - Identificación completa de las partes (nombre, CUIT/CUIL, domicilio, representación)

2. Antecedentes / considerandos (cuando el contexto lo justifica)

3. Objeto
   - Descripción precisa de la obligación principal
   - Indicación de si es de medios o de resultado

4. Precio y forma de pago
   - Monto, moneda, mecanismo de actualización si aplica
   [VERIFICAR RÉGIMEN CAMBIARIO VIGENTE] si hay moneda extranjera

5. Plazo
   - Fecha de inicio y vencimiento
   - Condiciones de prórroga si las hay

6. Obligaciones de cada parte
   - Detalladas, sin remisión genérica

7. Garantías (si aplica)
   - Tipo, alcance, inscripción si corresponde

8. Confidencialidad (si aplica)
   - Objeto, plazo determinado, excepciones estándar

9. Cláusula penal (si aplica)
   - Monto, carácter (compensatorio o punitorio), reducción judicial

10. Resolución del contrato
    - Pacto comisorio expreso o implícito
    - Procedimiento: intimación previa + plazo razonable (art. 1088 CCCN [VERIFICAR VIGENCIA])
    - Consecuencias de la resolución

11. Domicilio especial constituido en Argentina
    - Obligatorio para partes extranjeras o sin domicilio conocido en Argentina

12. Foro y ley aplicable
    - Verificar validez de la prórroga según el tipo de contrato
    - En contratos de consumo: foro competente según LDC; prórroga al extranjero inválida

13. Disposiciones generales
    - Integralidad del acuerdo
    - Modificaciones por escrito
    - Cesión (con o sin consentimiento)

14. Firma
    - Lugar, fecha, firma de las partes o representantes
    - Si hay representación: verificar poder suficiente
```

---

## Tipología de contratos - lógica de análisis por tipo

### Contratos de servicios profesionales

**Norma base:** arts. 1251-1279 CCCN (obra y servicios) [VERIFICAR VIGENCIA]

**Obligación:** de medios en general (el profesional se compromete a actuar con diligencia, no a un resultado). Excepción: prestaciones con resultado garantizado (peritaje, traducción jurada, certificación).

**Preguntas de diagnóstico:**
1. ¿La prestación es intuitu personae? ¿Se puede subcontratar?
2. ¿Hay exclusividad? (riesgo de relación laboral encubierta)
3. ¿Hay confidencialidad? ¿Con plazo determinado?
4. ¿Hay propiedad intelectual sobre el trabajo producido? ¿A quién pertenece?
5. ¿Cómo se determina el precio? ¿Hora, proyecto, resultado?

**Alertas específicas:**
- Exclusividad + horario + subordinación = señal de relación laboral. Alertar siempre.
- Propiedad intelectual: si el contrato no lo dice, la obra pertenece al autor (Ley 11.723 [VERIFICAR VIGENCIA]). Si el cliente quiere los derechos: cláusula de cesión expresa.
- Responsabilidad profesional: el estándar es el del "buen profesional" de la especialidad. No poner cláusulas que eleven el estándar a resultado sin justificación.

**Red-flags adicionales para este tipo:**
- Cláusula de "satisfacción del cliente" como condición de pago: convierte la obligación de medios en obligación de resultado unilateral.
- Ausencia de mecanismo de determinación de honorarios adicionales ante cambios de alcance (scope creep).

---

### Contratos de prestación de servicios tecnológicos / SaaS

**Normas base:** arts. 1251-1279 CCCN / LDC si hay consumidor / Ley 25.326 (privacidad) [VERIFICAR VIGENCIA]

**Preguntas de diagnóstico:**
1. ¿La contraparte es consumidor? (activa LDC y sus red-flags de nulidad)
2. ¿El servicio involucra tratamiento de datos personales? (activa Ley 25.326)
3. ¿El proveedor tiene sede en el extranjero? ¿Hay prórroga de jurisdicción?
4. ¿Hay SLA (niveles de servicio)? ¿Con penalidad por incumplimiento?
5. ¿Qué pasa con los datos del cliente si rescinde el contrato?

**Alertas específicas:**
- Prórroga de jurisdicción al extranjero en contratos de consumo: `[RED FLAG - NULIDAD ABSOLUTA]`
- Limitación de responsabilidad del proveedor por fallas del servicio sin excepción para dolo o culpa grave: `[RED FLAG - NULIDAD ABSOLUTA]` (art. 1743 CCCN [VERIFICAR VIGENCIA])
- Tratamiento de datos personales: verificar si el proveedor es "responsable del archivo" o "usuario del dato" bajo Ley 25.326. La distinción impacta en las obligaciones de seguridad y en quién responde ante el titular del dato.
- Modificación unilateral de precio o condiciones: cláusula abusiva en contrato de adhesión (art. 985 CCCN [VERIFICAR VIGENCIA]).

---

### Contratos de compraventa de bienes

**Norma base:** arts. 1123-1171 CCCN [VERIFICAR VIGENCIA]

**Preguntas de diagnóstico:**
1. ¿El bien es mueble o inmueble? (distintos requisitos formales)
2. ¿Hay tradición o se difiere? ¿Cuándo se transfiere la propiedad?
3. ¿Hay garantías por evicción o vicios ocultos?
4. ¿Hay precio a pagar en cuotas? ¿Con qué garantía?
5. ¿El bien está gravado (hipoteca, embargo, prenda)?

**Alertas específicas:**
- Inmuebles: el boleto de compraventa no transfiere el dominio; solo la escritura pública e inscripción registral (art. 1892 CCCN [VERIFICAR VIGENCIA]). Aclarar esto en el contrato para evitar expectativas erróneas.
- Vicios ocultos: la garantía opera de pleno derecho (arts. 1051-1058 CCCN [VERIFICAR VIGENCIA]); una cláusula que la excluya totalmente puede ser abusiva en contratos de adhesión.
- Precio en moneda extranjera: `[VERIFICAR RÉGIMEN CAMBIARIO VIGENTE]`
- Reserva de dominio en compraventa con precio diferido: verificar inscripción si corresponde.

---

### Contratos de locación

**Norma base:** arts. 1187-1226 CCCN + Ley 27.551 y modificatorias [VERIFICAR VIGENCIA: régimen al momento del contrato]

**Preguntas de diagnóstico:**
1. ¿Es locación urbana con destino habitacional o comercial? (distintos regímenes)
2. ¿El locatario es consumidor? (activa LDC)
3. ¿Cuál es el plazo? ¿Respeta el mínimo legal?
4. ¿Cómo se actualiza el precio? ¿Por qué índice?
5. ¿Qué garantías admite? (caución, seguro de caución, aval bancario, garantía personal)

**Alertas específicas:**
- Plazo mínimo: `[VERIFICAR VIGENCIA: Ley 27.551 - plazo mínimo vigente al momento del contrato]`
- Mecanismo de actualización del precio: `[VERIFICAR VIGENCIA: índice de actualización admitido por la norma vigente al momento del contrato]`
- Garantías no admitidas por la ley vigente: `[RED FLAG - NULIDAD ABSOLUTA: garantía no habilitada por Ley 27.551 - verificar norma vigente]`
- Cláusula de resolución sin intimación previa: `[RED FLAG - RIESGO ALTO: pacto comisorio sin procedimiento de intimación - art. 1088 CCCN]`

---

### Acuerdos de confidencialidad (NDA)

**Norma base:** arts. 957-983 CCCN / Ley 24.766 (confidencialidad) [VERIFICAR VIGENCIA]

**Preguntas de diagnóstico:**
1. ¿Es unilateral o bilateral?
2. ¿Qué información cubre? ¿Hay exclusiones estándar (información pública, obtenida de tercero, requerida judicialmente)?
3. ¿Cuál es el plazo? ¿Es razonable para el tipo de información?
4. ¿Hay cláusula penal? ¿El monto es proporcional al daño potencial?
5. ¿Hay obligación de devolver o destruir la información al vencer?

**Alertas específicas:**
- Plazo sin término o mayor a 5 años para información no constitutiva de secreto comercial: `[RED FLAG - RIESGO ALTO: confidencialidad sin plazo razonable - riesgo de nulidad parcial por indeterminación]`
- Ausencia de excepciones estándar: el NDA que no excluye la información pública o la requerida judicialmente crea obligaciones imposibles de cumplir.
- Obligación de confidencialidad sobre información que ya era pública al momento de la firma: nula de pleno derecho.

---

### Contratos de mutuo (préstamo de dinero)

**Norma base:** arts. 1525-1532 CCCN [VERIFICAR VIGENCIA]

**Preguntas de diagnóstico:**
1. ¿Hay interés pactado? ¿A qué tasa?
2. ¿La tasa es fija o variable? ¿Qué índice la actualiza?
3. ¿Hay garantía real (hipoteca, prenda) o personal (fianza, aval)?
4. ¿Qué pasa ante incumplimiento? ¿Hay interés punitorio?
5. ¿Es entre particulares o hay una entidad financiera involucrada?

**Alertas específicas:**
- Tasa usuraria: el CCCN no define un tope de tasa, pero la jurisprudencia reduce tasas que configuran lesión (art. 332 CCCN [VERIFICAR VIGENCIA]) o abuso del derecho. Verificar criterio del fuero.
- Interés compuesto (anatocismo): art. 770 CCCN [VERIFICAR VIGENCIA] lo prohíbe salvo excepciones. Alertar si el contrato lo prevé.
- Entidad financiera sin autorización BCRA: verificar si la actividad de préstamo requiere autorización.
- Garantía hipotecaria: requiere escritura pública e inscripción registral para ser oponible a terceros.

---

### Contratos de agencia, concesión y franquicia

**Norma base:** arts. 1479-1524 CCCN [VERIFICAR VIGENCIA]

**Preguntas de diagnóstico:**
1. ¿Cuál de los tres tipos es? (las obligaciones del principal difieren sustancialmente)
2. ¿Hay zona exclusiva? ¿Está delimitada con precisión?
3. ¿Hay cuotas mínimas de compra o venta?
4. ¿Qué pasa con el stock y la marca al terminar el contrato?
5. ¿Hay compensación por clientela al agente?

**Alertas específicas:**
- Agencia: el agente tiene derecho a compensación por clientela al terminar el contrato (art. 1497 CCCN [VERIFICAR VIGENCIA]) salvo extinción por incumplimiento del agente. Alertar si el contrato intenta renunciar a este derecho.
- Concesión y franquicia: verificar si hay aportes del concesionario o franquiciado que generen derecho de reembolso al terminar.
- No competencia post-contractual: verificar plazo y ámbito geográfico razonables.

---

## Reglas de citación - contratos

Las reglas del CLAUDE.md argentino aplican íntegramente. Específicas para contratos:

**Normas del CCCN:** primera mención siempre con `[VERIFICAR VIGENCIA]`. Para contratos anteriores al 1° de agosto de 2015:
```
[VERIFICAR RÉGIMEN APLICABLE: contrato anterior al CCCN - determinar si aplica CC/CCom o CCCN]
```

**Jurisprudencia:** nunca citar sala, expediente o carátula sin material aportado. Usar:
```
[INSERTAR FALLO VERIFICADO: doctrina requerida - aportar expediente, sala, fuero y año]
```

**Régimen cambiario:** ante cualquier obligación en moneda extranjera:
```
[VERIFICAR RÉGIMEN CAMBIARIO VIGENTE: normativa BCRA]
```

**Relación laboral encubierta:** si hay indicios, no continuar la revisión del contrato como si fuera civil sin antes alertar:
```
[VACÍO PROBATORIO: existencia de relación de dependencia encubierta - verificar con el abogado antes de continuar el análisis como contrato civil]
```

---

## Instrucciones operativas específicas - contratos

- Clasificar siempre (adhesión / paritario / consumidor / laboral encubierto) antes de analizar cláusula por cláusula.
- Correr el análisis de red-flags completo antes de cualquier modificación o redacción.
- En contratos de adhesión con consumidor: interpretar siempre en favor del consumidor (art. 1094 CCCN / art. 3 LDC [VERIFICAR VIGENCIA]).
- En contratos de larga duración (más de 6 meses): verificar siempre si hay mecanismo de actualización de precio. Si no hay: marcar como `[RED FLAG - RIESGO ALTO]`.
- No redactar cláusula de confidencialidad sin plazo determinado. Si el abogado pide plazo indefinido: informar el riesgo y proponer plazo razonable con cláusula de renovación.
- Cláusula penal: verificar que el monto sea proporcional al daño potencial (art. 794 CCCN [VERIFICAR VIGENCIA]). Si es manifiestamente excesiva: alertar.
- Garantías: verificar siempre si requieren inscripción registral para ser oponibles a terceros.
- Todo informe de revisión y todo borrador de contrato cierra con "Estado del análisis":
  1. Red-flags detectadas con marcador y desarrollo.
  2. Normas con `[VERIFICAR VIGENCIA]`: listado.
  3. Marcadores `[VACÍO PROBATORIO]` o `[INSERTAR FALLO VERIFICADO]` pendientes.
  4. Decisiones estructurales por defecto que el abogado debe confirmar.

---

*Última actualización: mayo 2026*
*Normativa base: CCCN (Ley 26.994), LDC (Ley 24.240), Ley 27.551 y modificatorias,
Ley 25.326, Ley 24.766, Ley 11.723*
*Archivo complementario obligatorio: `argentina/red-flags-contratos.md`*
*Autor: Dr. Cristian Aboitiz · [@abogadoaboitiz](https://x.com/abogadoaboitiz)*

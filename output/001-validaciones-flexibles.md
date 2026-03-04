# Metadata
- **Slug:** validaciones-flexibles-software
- **Title:** Validaciones flexibles en software: cuando el negocio no encaja en reglas rígidas
- **Meta:** Descubre por qué las validaciones rígidas en software fallan en la realidad y cómo diseñar reglas flexibles que se adapten al negocio real.
- **Tag:** Desarrollo
- **Date:** 2026-03-04
- **Read time:** 7

# Contenido

## El problema de las validaciones absolutas

Cuando desarrollamos software, la tentación natural es pensar en blanco y negro. Si el paciente no pagó las cuotas necesarias, no puede pedir el siguiente frasco de tratamiento. Punto. La regla es clara, limpia, fácil de programar.

Hasta que llega la realidad.

En un proyecto reciente de digitalización para un consultorio médico, nos encontramos con un escenario clásico: la secretaria necesitaba pedir un frasco de tratamiento para un paciente que aún debía cuotas. ¿La razón? El paciente iba a pagar la semana siguiente, pero el frasco tarda 30 días en llegar del laboratorio. Si esperaban al pago, el tratamiento se retrasaba un mes entero.

La regla de negocio decía "no". La realidad del negocio decía "sí, pero con cuidado".

## Validación dura vs. validación flexible

En ingeniería de software existen dos enfoques para manejar reglas de negocio:

- **Validación dura (hard validation):** El sistema bloquea la acción. No hay forma de continuar sin cumplir la condición. Es simple y segura, pero inflexible.
- **Validación flexible (soft validation):** El sistema advierte, pero permite continuar con una acción consciente del usuario. Registra que se hizo una excepción y por qué.

La validación dura funciona perfecto cuando la regla es absoluta: no podés vender un producto con stock cero, no podés registrar una fecha de nacimiento futura. Pero muchas reglas de negocio no son absolutas — son **guías operativas** que admiten excepciones controladas.

## Cómo lo resolvimos

En nuestro caso, el flujo quedó así:

1. **El sistema detecta la deuda:** Cuando la secretaria intenta pedir un frasco y el paciente debe cuotas, aparece un aviso claro: "Este paciente debe 2 cuotas".
2. **Ofrece la opción de continuar:** Un botón "Pedir igualmente" permite avanzar, pero no es el camino por defecto.
3. **Pide una justificación:** Se abre un campo de texto para registrar el motivo ("Paciente paga la semana que viene, frasco tarda 30 días").
4. **Marca visualmente la excepción:** El frasco queda con un indicador naranja de "deuda pendiente" hasta que se salden las cuotas.
5. **Se actualiza automáticamente:** Cuando el paciente paga, el indicador desaparece solo. La nota histórica permanece.

El punto clave es que **nadie tiene que acordarse de nada**. El sistema se encarga de rastrear la deuda y de limpiarla cuando se resuelve.

## Por qué importa el diseño de la excepción

Un error común es tratar las excepciones como ciudadanos de segunda clase. Si vas a permitir que el usuario se salte una regla, hacelo bien:

- **Que sea visible pero no el camino por defecto.** No queremos que el usuario siempre se salte la validación. El flujo normal debe ser cumplir la regla.
- **Que quede registrado.** Cada excepción debe tener un rastro: quién, cuándo, por qué. Esto no es para castigar — es para aprender y mejorar los procesos.
- **Que se resuelva sola cuando la condición cambie.** Si la deuda se salda, el sistema debe reflejarlo automáticamente. Nada de "acordate de ir a actualizar el estado del frasco".
- **Que el lenguaje sea claro.** No "Error 4502: violación de constraint FK_cuotas". Sino "Este paciente debe 2 cuotas. ¿Querés pedir el frasco igualmente?"

## El impacto en usuarios no técnicos

Este punto es crucial cuando tu usuario final es una secretaria de consultorio, no un programador. La interfaz tiene que comunicar tres cosas en un segundo:

1. **Qué pasa** — "Hay una deuda"
2. **Qué significa** — "Normalmente no se pediría el frasco"
3. **Qué puede hacer** — "Pero podés pedirlo igual si tenés un motivo"

Sin jerga técnica, sin códigos de error, sin pantallas rojas que asustan. Un cartel naranja con lenguaje humano y un botón que dice exactamente lo que hace.

## Cuándo usar cada tipo de validación

No toda regla merece ser flexible. Una guía práctica:

**Usá validación dura cuando:**
- La acción es irreversible (eliminar datos permanentemente)
- Hay riesgo legal o regulatorio (facturación, datos médicos sensibles)
- La regla es física o lógica, no operativa (no podés agendar antes de ayer)

**Usá validación flexible cuando:**
- La regla es operativa y admite excepciones justificadas
- El usuario tiene contexto que el sistema no tiene
- Bloquear la acción genera más problemas que permitirla con control
- Hay un mecanismo automático para resolver la excepción después

## Conclusión

El software más útil no es el que tiene más reglas — es el que entiende cuándo una regla es guía y cuándo es ley. Diseñar validaciones flexibles requiere más trabajo que simplemente bloquear, pero el resultado es un sistema que se adapta al negocio real en lugar de obligar al negocio a adaptarse al sistema.

En <a href="/">NOUD</a> trabajamos con este enfoque: entender primero cómo opera realmente el negocio, y después diseñar la tecnología que lo potencia. Si estás digitalizando procesos y sentís que el software te limita en vez de ayudarte, probablemente es hora de revisar dónde las reglas son demasiado rígidas.

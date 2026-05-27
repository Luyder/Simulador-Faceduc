# Plan de Proyección Financiera - Simulador de Financiamiento

Simulador interactivo para explorar opciones de financiamiento educativo (Pregrados y Posgrados) usado por la Facultad de Educación.

## Resumen rápido (qué hace el simulador)
- Permite comparar y simular flujos de caja mensuales para distintas opciones de apoyo financiero.
- Genera un cronograma mes a mes, muestra cuotas de matrícula, capital, intereses y saldo.
- Incluye controles para ajustar porcentaje a financiar, seleccionar programas de posgrado y modalidades de apoyo.

## Reglas y supuestos principales (actualizado)

### Pregrados
- La pestaña **Pregrados** agrupa los dos productos disponibles: **Apoyo 2048** y **Apoyo CP**. Seleccioná cuál deseas simular.

- **Apoyo 2048 (Pregrado)**
   - Tope máximo de financiamiento: **95%** del valor base por semestre.
   - Composición: **40%** del monto financiado se amortiza durante el periodo de estudios; **60%** se difiere y se amortiza después del estudio.
   - Durante el estudio: la parte 40% se amortiza en los meses de estudio (distribuida por semestre) y, además, **se cobran intereses mensuales sobre la parte diferida (60%)** aunque su capital se pague después.
   - Plazo post‑estudio (para la parte 60%): se establece como máximo el doble de la duración financiada. Ejemplo: programa de 48 meses → post‑plazo = 96 meses. La vista del cronograma muestra estudio + post‑estudio (48 + 96 = 144 meses en este caso).
   - Tasa aplicada durante todos los cálculos: **1.0% M.V.** (mensual vencido).

- **Apoyo CP (Corto Plazo, Pregrado)**
   - Tope máximo de financiamiento: **75%** por semestre.
   - Cada semestre financiado se amortiza en **5 cuotas mensuales** iguales (fórmula francesa), por lo que las cuotas son cortas y puntuales.
   - Tasa: **1.1% M.V.**
   - La vista del cronograma para CP muestra el horizonte equivalente a la duración del estudio clásico (8 semestres × 6 meses = **48 meses**).

### Posgrados
- Valor por crédito: **1.867.000 COP**.
- Programas incluidos (ejemplos): másteres y especializaciones con asignación de créditos por semestre (el simulador toma una distribución fija por programa).
- Opciones de apoyo:
   - **Vega Lara — Corto**: amortiza cada desembolso semestral en **5 meses**. Tasa: **1.0% M.V.**
   - **Vega Lara — Mediano**: durante el estudio se pagan **intereses mensuales sobre el saldo acumulado** y se cobra un **aval del 2%** por cada desembolso semestral; el capital se amortiza después del estudio en el plazo configurado (por defecto 48 meses en la rama original, pero puede adaptarse). Tasa: **1.3% M.V.**
   - **Progresandes**: modalidad corta (similar a Vega corto) y solo disponible para ciertos programas (por ejemplo `esp_liderazgo`). Tasa: **1.0% M.V.**

## Cómo leer el cronograma
- La tabla muestra cada mes con columnas: Matrícula (copago), Capital (amortización), Intereses, Total y Saldo.
- Para Pregrados:
   - **CP**: cronograma hasta 48 meses (8 semestres × 6 meses).
   - **2048**: cronograma hasta estudio + post‑estudio (por ejemplo 48 + 96 = 144 meses si se financia 48 meses).
- Para Posgrados: cronograma por semestre y por mes según la modalidad elegida; las matrículas se muestran en el mes de inicio de cada semestre.

## Controles importantes en la UI
- Slider `% a Financiar`: ajusta el porcentaje de cada semestre que se financia (límite 95% para 2048, 75% para CP, 0–100% para posgrados según reglas).
- Selección de `Pregrados` → elegir entre `Apoyo 2048` y `Apoyo CP`.
- Selección de `Posgrados` → elegir programa, porcentaje a financiar y tipo de apoyo (Vega corto/mediano o Progresandes si aplica).

## Fórmulas y supuestos técnicos
- Amortización francesa (cuota fija) utilizada para las partes amortizadas en plazos cortos o post‑estudio.
- Intereses calculados mensualmente sobre el saldo vigente (tasa M.V.).
- Para 2048, durante los estudios **se cobran intereses sobre la parte 60% diferida** aunque su capital sea amortizado después.

## Ejemplos rápidos (actualizados)
- **Pregrado — 2048 (ej.)**
   - Duración de estudio: 48 meses (8 semestres)
   - Post‑plazo = 96 meses (2× duración)
   - Cronograma mostrado: 48 + 96 = **144 meses**
   - Tasa: 1.0% M.V. — para entender impacto anual, TEA ≈ (1+0.01)^12−1 ≈ 12.7%.

- **Pregrado — CP (ej.)**
   - Horizonte mostrado: **48 meses**
   - Cada semestre financiado amortizado en 5 meses.
   - Tasa: 1.1% M.V.

- **Posgrado — Vega Mediano (ej.)**
   - Durante estudio: se pagan intereses sobre saldo acumulado + aval 2% en cada desembolso.
   - Post‑estudio: capital amortizado en plazo definido (por defecto 48 meses en la versión original; el simulador puede ajustarlo según reglas de producto).

## Cómo ejecutar
1. Abrir `index2.html` en un navegador moderno (el simulador principal está en `index2.html` para la versión con posgrados).
2. Usar la UI para cambiar pestañas (`Pregrados` / `Posgrados`), seleccionar producto y ajustar sliders.

## Notas de diseño y mantenimiento
- La lógica de cálculos está en `index2.html` dentro del componente `SimuladorFinanciero` (hooks `useMemo`): `datos2048`, `datosCP`, `datosPosgrado`.
- Si modificás reglas (tasas, plazos, límites), actualizar también las constantes correspondientes en `index2.html`.

## Licencia y contacto
- Proyecto educativo de la Facultad de Educación — Universidad de los Andes.

---
**Última actualización:** 2026-05-27
**Versión:** 1.1
**Versión:** 1.0

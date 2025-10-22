# Resumen: Algoritmo FOIL (First Order Inductive Learner)

## 🎯 Objetivo

El algoritmo FOIL es una técnica de aprendizaje inductivo que evalúa qué tan útil es una condición para separar ejemplos positivos de ejemplos negativos en un conjunto de datos.

## 📐 Fórmula del FOIL Gain

```
FOIL Gain = p × (log₂(p/(p+n)) - log₂(P/(P+N)))
```

### Variables:
- **P**: Total de ejemplos **positivos** ANTES de aplicar la condición
- **N**: Total de ejemplos **negativos** ANTES de aplicar la condición
- **p**: Ejemplos **positivos** que cumplen la condición (DESPUÉS)
- **n**: Ejemplos **negativos** que cumplen la condición (DESPUÉS)

## 🔍 Interpretación

- **FOIL Gain > 0**: La condición es útil, mejora la separación de clases
- **FOIL Gain = 0**: La condición no aporta información
- **FOIL Gain < 0**: La condición empeora la clasificación

**Mayor FOIL Gain = Mejor condición discriminante**

## 💡 Casos Analizados

### Caso 1: Condición Categórica
**Condición**: `nivel_educativo == 'terciario'`

| Métrica | Valor |
|---------|-------|
| P (positivos totales) | 4 |
| N (negativos totales) | 4 |
| p (positivos capturados) | 3 |
| n (negativos capturados) | 0 |
| **FOIL Gain** | **3.000** |

**Interpretación**: Excelente condición. Captura 3 de 4 positivos sin capturar ningún negativo (pureza 100%).

### Caso 2: Condición Numérica
**Condición**: `edad <= 23`

| Métrica | Valor |
|---------|-------|
| P (positivos totales) | 4 |
| N (negativos totales) | 4 |
| p (positivos capturados) | 3 |
| n (negativos capturados) | 0 |
| **FOIL Gain** | **3.000** |

**Interpretación**: Igual de efectiva que la condición anterior. Ambas logran la misma discriminación.

## 📊 Paso a Paso del Cálculo

### Ejemplo: `nivel_educativo == 'terciario'`

1. **Conteo inicial**:
   - P = 4, N = 4 (balance 50-50)

2. **Aplicar condición**:
   - p = 3, n = 0 (3 positivos, 0 negativos)

3. **Calcular proporciones**:
   - Antes: P/(P+N) = 4/8 = 0.5
   - Después: p/(p+n) = 3/3 = 1.0

4. **Calcular logaritmos**:
   - log₂(1.0) = 0
   - log₂(0.5) = -1

5. **FOIL Gain**:
   - 3 × (0 - (-1)) = 3 × 1 = **3.0**

## ✅ Ventajas del FOIL

- ✓ Cuantifica objetivamente la utilidad de cada condición
- ✓ Funciona con atributos categóricos y numéricos
- ✓ Penaliza condiciones que capturan muchos negativos
- ✓ Prioriza alta cobertura de positivos con alta pureza

## ⚠️ Consideraciones

- El FOIL Gain favorece condiciones que capturan muchos positivos (factor **p**)
- Una condición con p=1, n=0 tendrá menor gain que p=3, n=0 (aunque ambas tengan pureza 100%)
- Se debe balancear entre cobertura (cantidad de positivos) y precisión (pureza)

## 🔗 Relación con Árboles de Decisión

FOIL Gain es similar a la **Ganancia de Información** usada en árboles de decisión (ID3, C4.5), pero:
- FOIL evalúa **condiciones individuales**
- Ganancia de Información evalúa **atributos completos** con todos sus valores

Ambos buscan lo mismo: maximizar la separación entre clases.

## 🎓 Aplicación Práctica

**Problema**: Identificar personas en formación

**Reglas descubiertas con FOIL Gain = 3.0**:
1. `SI nivel_educativo == 'terciario' ENTONCES en_formacion = True`
2. `SI edad <= 23 ENTONCES en_formacion = True`

Ambas reglas son igualmente efectivas para el dataset analizado.

---

**Conclusión**: El FOIL Gain es una métrica poderosa para inducción de reglas que permite evaluar objetivamente qué condiciones son más útiles para clasificar datos, priorizando aquellas que maximizan la cobertura de positivos manteniendo alta pureza.

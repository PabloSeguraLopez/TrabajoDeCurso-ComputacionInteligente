# Simulación de Incendio Forestal en Bosque Canario con Vientos Alisios

## Descripción general

Este proyecto implementa un modelo de incendio forestal basado en agentes estáticos en NetLogo, diseñado para representar un bosque canario heterogéneo sometido a vientos alisios dominantes (NE → SW).  

El modelo se inspira en enfoques clásicos de autómatas celulares para incendios forestales, introduciendo como extensión principal una influencia direccional explícita del viento, así como heterogeneidad en **tipos de vegetación, humedad del combustible y propagación por pavesas (ember spotting).

Cada parche del entorno representa una porción fija del terreno que puede encontrarse en distintos estados (suelo, vegetación, fuego o quemado).

## Características principales

- Modelo basado en agentes estáticos
- Tres tipos de vegetación:
  - Laurisilva
  - Pinar canario
  - Matorral
- Humedad del combustible dependiente del tipo de vegetación, con ruido estocástico
- Propagación del fuego:
  - Probabilística
  - Dependiente de humedad, viento y pendiente
- Vientos alisios modelados como un sesgo direccional continuo
- Propagación secundaria por pavesas transportadas por el viento
---

## Estados del modelo

Cada parche puede encontrarse en uno de los siguientes estados:

| Estado | Significado        |
|------:|--------------------|
| 0     | Suelo sin vegetación |
| 1     | Vegetación          |
| 2     | En combustión       |
| 3     | Área quemada        |

---

## Parámetros principales

Todos los parámetros están declarados directamente en el código:

- **Cobertura forestal y composición**
  - `forest-cover`
  - `laurel-fraction`, `pine-fraction`, `shrub-fraction`

- **Humedad del combustible**
  - `base-moisture-*`
  - `moisture-noise`

- **Carga de combustible**
  - `fuel-*`
  - `burn-rate`

- **Propagación del fuego**
  - `base-spread`
  - Influencia del viento (`wind-dir`, `wind-strength`)
  - Influencia de la pendiente (`use-slope?`, `slope-strength`)

- **Propagación por pavesas**
  - `ember-spotting?`
  - `ember-rate`
  - `ember-distance-max`
  - `ember-ignite-bonus`

---

## Dinámica del modelo

1. **Inicialización**
   - Generación del paisaje forestal
   - Asignación de tipos de vegetación y humedad
   - Definición del punto de ignición inicial
   - Inicialización de vientos alisios

2. **Evolución temporal**
   - Propagación del fuego a parches vecinos
   - Consumo progresivo del combustible
   - Posible ignición a distancia por pavesas
   - Finalización automática cuando no queda fuego activo

## Ejecución
![Ejecución](Fuego-con-alisios.gif)


## Referencias

- NetLogo Models Library. *Fire* y *Fire Simple* models.  
  Wilensky, U. Center for Connected Learning and Computer-Based Modeling, Northwestern University.

## Uso de Inteligencia Artificial
En este trabajo se han usado herramientas de inteligencia artificial para:
- Barajar qué parámetros se podrían utilizar en la simulación, decidiendo añadir alguno de los que estas herramientas enunciaban y quitar alguno de los que el estudiante proponía para mejorar realismo.
- Seleccionar la configuración inicial de los valores de esos parámetros, para tener un punto de partida. Los valores que se usaron finalmente en los experimentos no fueron los generados por la IA, sino unos seleccionados por el estudiante, guiándose parcialmente por ese punto de partida.


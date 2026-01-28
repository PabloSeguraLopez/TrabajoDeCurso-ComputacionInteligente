# Modelo Depredadores–Presas  
## Lobos – Ovejas – Hierba con Flocking y Refugios (NetLogo)

## Descripción general

Este modelo implementa una extensión del clásico sistema **depredador–presa** en NetLogo, basado en lobos y ovejas que interactúan en un entorno con **hierba renovable**, **comportamiento de flocking** en las ovejas y **refugios espaciales** que limitan la caza.

El objetivo principal es explorar dinámicas poblacionales emergentes cuando se introducen:
- Movimiento colectivo (flocking),
- Zonas seguras (refugios),
- Visión limitada,
- Costes energéticos y reproducción probabilística.


## Agentes y entorno

### Agentes

- **Ovejas**
  - Se alimentan de hierba.
  - Huyen de los lobos si los detectan.
  - Pueden moverse en flock (cohesión, alineamiento y separación).
  - Se reproducen con una probabilidad dada.
  - Mueren si su energía llega a cero.

- **Lobos**
  - Cazan ovejas.
  - Persiguen a la oveja más cercana dentro de su radio de visión.
  - No pueden entrar en parches refugio (si están activados).
  - Obtienen energía al cazar.
  - Se reproducen con una probabilidad dada.
  - Mueren si su energía llega a cero.

### Parches

Cada parche puede ser:
- **Hierba (`grass?`)**: fuente de alimento para las ovejas.
- **Refugio (`refuge?`)**: zona segura donde los lobos no pueden entrar. Puede tener hierba.
- **Hierba agotada**: vuelve a crecer tras un tiempo de regeneración.


## Variables principales

### Globales

- `initial-wolves`: número inicial de lobos.
- `initial-sheep`: número inicial de ovejas.
- `grass-regrow-time`: tiempo de regeneración de la hierba.
- `refuge-density`: porcentaje de parches que serán refugios.
- `wolf-vision`, `sheep-vision`: radios de percepción.
- `sheep-step`, `wolf-step`: velocidad de movimiento.
- `sheep-gain-from-grass`: energía obtenida al comer.
- `wolf-gain-from-food`: energía obtenida al cazar.
- `sheep-reproduce-prob`, `wolf-reproduce-prob`: probabilidades de reproducción (%).
- `flocking?`: activa o desactiva el comportamiento colectivo de las ovejas.
- `use-refuges?`: activa o desactiva los refugios.

### Variables propias

- **Tortugas**
  - `energy`: energía del agente.

- **Parches**
  - `grass?`: indica si hay hierba.
  - `countdown`: tiempo restante para que vuelva a crecer la hierba.
  - `refuge?`: indica si el parche es refugio.


## Dinámica del modelo

### Ciclo principal (`go`)

En cada tick:
1. Las ovejas:
   - Se mueven (huida y flocking/paseo).
   - Comen hierba.
   - Se reproducen.
   - Pierden energía por metabolismo.
2. Los lobos:
   - Se mueven (caza o patrullaje).
   - Cazan ovejas si comparten parche.
   - Se reproducen.
   - Pierden energía por metabolismo.
3. La hierba vuelve a crecer donde fue consumida.
4. Se incrementa el contador de tiempo.

La simulación se detiene si desaparecen todas las ovejas o todos los lobos.


## Comportamientos clave

### Flocking de ovejas
Incluye:
- **Separación**: evitar colisiones.
- **Alineamiento**: ajustar la dirección al promedio del grupo.
- **Cohesión**: moverse hacia el centro de masa del grupo.

### Refugios
- Son parches inaccesibles para los lobos.
- Las ovejas pueden entrar y alimentarse allí.
- Introducen variaciones en el terreno (pueden verse como montañas).

## Ejecución
![Ejecución](VideoAgentesMoviles.gif)


## Referencias

- Modelo clásico Lobos–Ovejas–Hierba (NetLogo Models Library).
- Boids / Flocking (Reynolds, 1987).

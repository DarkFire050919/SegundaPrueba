# Documentación de `Aspiradora 1.py`

## Visión General
`Aspiradora 1.py` implementa una simulación simple de una **aspiradora (agente) y un entorno** compuesto por dos **cuartos**. El objetivo es demostrar un agente con lógica de limpieza básica y movimiento. El agente verifica el estado del cuarto, limpia si es sucio y se desplaza entre los dos cuartos.

## Estructura del Código

### 1. Clase `Ambiente`
| Atributo | Tipo | Descripción |
|---|---|---|
| `cuartos` | `list[int]` | Lista de dos índices representando el estado de cada cuarto: `1` = sucio, `0` = limpio. La posición inicial del agente es el cuarto `0` (el primero). |

#### Métodos
| Método | Parámetros | Retorno | Descripción |
|---|---|---|---|
| `step(position: int) -> int` | `position` – índice del cuarto a inspeccionar | Estado del cuarto (1 o 0) | Devuelve el estado del cuarto correspondiente. |
| `aplicar(position: int, suciedad: int)` | `position`, `suciedad` | None | Actualiza el estado de `cuartos[position]` a `suciedad` (0 o 1). |

---

### 2. Clase `AgenteAspiradora`
| Atributo | Tipo | Descripción |
|---|---|---|
| `posicion` | `int` | Índice del cuarto actual. Inicialmente `0`. |
| `izq` | `int` | Moverse a la izquierda: `-1`. |
| `der` | `int` | Moverse a la derecha: `+1`. |

#### Métodos
| Método | Parámetros | Retorno | Descripción |
|---|---|---|---|
| `sensar(ambiente: Ambiente) -> int` | `ambiente` – objeto `Ambiente` | Estado (`1` o `0`) | Llama a `ambiente.step(self.posicion)` y devuelve el estado. También imprime una trazabilidad.
| `actuar(ambiente: Ambiente, estado: int)` | `ambiente`, `estado` | None | Si `estado == 1` limpia el cuarto (`ambiente.aplicar(self.posicion, 0)`). Luego imprime la acción de movimiento: si está en el cuarto 0 mueve a la derecha, de lo contrario a la izquierda. |

---

### 3. Simulación Principal
```python
ambiente_obj = Ambiente()
aspiradora_obj = AgenteAspiradora()

for _ in range(5):
    estado = aspiradora_obj.sensar(ambiente_obj)
    aspiradora_obj.actuar(ambiente_obj, estado)
```

- Se crea una instancia de `Ambiente` y `AgenteAspiradora`.
- Se ejecuta un bucle de 5 iteraciones que:
  1. Lee el estado del cuarto actual.
  2. Actúa: limpia si es necesario y cambia de cuarto.

#### Salida Esperada
Cada iteración genera una salida similar a:
```
Sensado posición 0: 1
Limpiar
Moviéndose a la derecha
Sensado posición 1: 1
Limpiar
Moviéndose a la izquierda
...
```

### 4. Posibles Extensiones
- **Números de cuartos**: usar un tamaño dinámico de lista en `Ambiente`.
- **Algoritmo más complejo**: introducir estados de batería, sensores de suciedad parcial, etc.
- **Persistencia**: guardar el estado en archivo o base de datos.

## Diagrama de Flujo (Mermaid)
Puedes generar un diagrama visual con Mermaid para entender el ciclo de sensado‑acción:

```mermaid
flowchart TD
  A[Inicio] --> B[Ambiente.step(pos)]
  B --> C{Valida si es sucio?}
  C -- Si --> D[Ambiente.aplicar(pos, 0)]
  C -- No --> D
  D --> E[Movimiento]
  E --> F{¿pos=0?}
  F -- Si --> G[pos = pos + 1]
  F -- No --> H[pos = pos - 1]
  G --> I[Regresar a B]
  H --> I
```

Se puede generar el PNG con la herramienta `create_mermaid_diagram`.

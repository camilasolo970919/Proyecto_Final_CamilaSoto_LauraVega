# Surtido por tienda con estimación de demanda y sustitución

Proyecto final de Aprendizaje de Máquina II, por Camila Soto y Laura Vega. Recrea el procedimiento del artículo de Fisher y Vaidyanathan (2014), *A Demand Estimation Procedure for Retail Assortment Optimization with Results from Implementations*, Management Science ([DOI 10.1287/mnsc.2014.1904](https://doi.org/10.1287/mnsc.2014.1904)).

El artículo responde esta pregunta: una cadena tiene un espacio limitado en el estante para una categoría y debe decidir qué productos pone en cada tienda. Para eso estima la demanda de cada producto en cada tienda, incluidos los que hoy no vende, y la probabilidad de que un cliente sustituya su producto favorito cuando no lo encuentra.

## Qué hace el proyecto

1. Simula las ventas de una cadena de 140 tiendas y 92 productos posibles, con los parámetros que reporta el artículo para la categoría de ponqués. Los datos originales no están publicados.
2. Estima la demanda y la sustitución de cada tienda por máxima verosimilitud.
3. Valida las estimaciones con un periodo que el modelo no vio.
4. Optimiza el surtido con la heurística greedy, para toda la cadena y por tienda.
5. Agrupa las tiendas según el surtido que más les conviene y mide el beneficio de localizar.
6. Pronostica las ventas de un producto nuevo.
7. Aplica el mismo procedimiento a datos públicos de yogur (The Complete Journey, de dunnhumby).

## Estructura

```
├── README.md
├── requirements.txt
├── data/          # datos simulados y datos públicos descargados
├── notebooks/     # notebook principal
│   └── recreacion_fisher_vaidyanathan.ipynb
├── src/           # funciones de apoyo (Python)
├── results/       # tablas de resultados
├── figures/       # gráficas generadas
└── references/    # artículo y material complementario
```

Las carpetas `data`, `results` y `figures` se llenan al ejecutar el notebook. Las funciones del modelo están definidas por ahora dentro del notebook, en la sección 2.

## Cómo reproducirlo

El notebook se ejecutó con Python 3.13.

```bash
python -m venv .venv
source .venv/bin/activate        # en Windows: .venv\Scripts\activate
pip install -r requirements.txt
jupyter notebook notebooks/recreacion_fisher_vaidyanathan.ipynb
```

Ejecute todas las celdas en orden. La semilla está fija, así que los resultados son siempre los mismos. La estimación tienda por tienda corre en paralelo y puede tardar varios minutos.

La sección 13 descarga dos archivos del repositorio público [completejourney](https://github.com/bradleyboehmke/completejourney) la primera vez que se ejecuta, por lo que necesita conexión a internet. Esos archivos quedan en `data/` y no se suben al repositorio.

## Archivos que genera

| Carpeta | Archivo | Contenido |
|---|---|---|
| `data/` | `ventas_simuladas.csv` | unidades por periodo, tienda y producto |
| `data/` | `productos_simulados.csv` | catálogo con atributos y precio |
| `data/` | `tiendas_simuladas.csv` | tabla de tiendas |
| `results/` | `clusters_tiendas.csv` | grupo asignado a cada tienda |
| `results/` | `comparacion_articulo.csv` | resultados del artículo frente a la recreación |
| `figures/` | `01_exploracion.png` | exploración de los datos simulados |
| `figures/` | `02_ingreso_vs_tamano.png` | ingreso capturado según el tamaño del surtido |
| `figures/` | `03_beneficio_localizacion.png` | beneficio de localizar según el número de surtidos |

## Referencia

Fisher, M., y Vaidyanathan, R. (2014). A Demand Estimation Procedure for Retail Assortment Optimization with Results from Implementations. *Management Science*, 60(10), 2401–2415.

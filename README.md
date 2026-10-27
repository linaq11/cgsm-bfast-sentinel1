# BFAST Monitor sobre Sentinel-1 banda C en el manglar de la Ciénaga Grande de Santa Marta

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.23709979.svg)](https://doi.org/10.5281/zenodo.23709979)
[![Ver Dashboard HTML](https://img.shields.io/badge/Ver-Dashboard%20HTML-orange?logo=html5&logoColor=white)](https://linaq11.github.io/cgsm-bfast-sentinel1/dashboard-percepcion-remota.html)

Estudio desarrollado en la Maestría en Geomática de la Universidad Nacional de Colombia (2026).

Aplicación de BFAST Monitor (Verbesselt et al. 2012) a series mensuales VH de Sentinel-1 banda C sobre las cinco estaciones permanentes CARICOMP del INVEMAR (período histórico 2020-2021, monitoreo 2022-2023). El algoritmo detectó cambios estructurales significativos entre abril 2022 y octubre 2023 con magnitudes entre 0.35 y 1.73 dB. La alerta del modelo en Aguas Negras precedió en seis meses al inicio del período de pérdida del 33 % del arbolado reportado por INVEMAR (ITF 2023), demostrando que SAR banda C, que no resuelve la pregunta de estado estructural instantáneo (componente A), sí responde a la pregunta de detección de cambio temporal.

- **Autor:** Lina María Quintero Fonseca · lquinterof@unal.edu.co
- **Fecha:** Mayo 2026

El informe completo de este trabajo forma parte de la tesis de maestría en curso de la autora y se publicará con ella; este repositorio contiene el código, los resultados tabulados y las figuras que lo sustentan.

## Estructura del repositorio

- `dashboard-percepcion-remota.html` — tablero interactivo de resultados (abrir vía badge superior)
- `scripts/` — pipelines Python (BFAST Monitor, AoA, GPBoost), scripts GEE de exportación, cuaderno R canónico de BFAST
- `figuras/` — figuras del cuerpo y de los anexos
- `data/` — outputs reproducibles (CSV, JSON, predicciones por parcela)

## Datos no incluidos

Por tamaño no se versionan los rasters originales (>50 MB cada uno):
- `CGSM_AoA_Stack_2023*.tif` (~3.9 GB) — exportar desde GEE con `scripts/CGSM_AoA_Export_Stack.js`
- `CGSM_Classification_*.tif` (~250 MB c/u) — exportar con `scripts/CGSM_Classification_Export.js`
- `aoa_di_2023.tif` (~138 MB) — generado por `scripts/compute_aoa.py`

## Reproducir el análisis

1. Ejecutar los scripts `.js` en Google Earth Engine para exportar stacks y muestras
2. Correr `scripts/compute_aoa.py`, `scripts/run_gpboost.py`, `scripts/bfast_bootstrap.py` y `scripts/bfast_monitor.py` en Python 3.10+ con las dependencias del contenedor sig_unal
3. La validación cruzada del Anexo H se reproduce con `scripts/bfast_monitor.Rmd` directamente en R

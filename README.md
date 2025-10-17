

# Informe de Gerencia – S&P 500 (Colab)



Análisis **ejecutable** del S&P 500 orientado a **dirección/gerencia**, diseñado para correr **100% con datos locales** (sin internet ni APIs) en **Google Colab**. El cuaderno genera un **informe ejecutivo**: panorama del índice, desempeño sectorial, líderes/rezagados, liquidez y volatilidad, correlaciones, drawdowns y conclusiones accionables.

---

## ✨ Características clave

- **Portada** y **correo simulado del “jefe”** con fecha automática.
- **Parámetros editables**: rango de fechas, sector/símbolos foco, ventanas móviles.
- **Carga de datos desde Google Drive** (CSV locales) con **fallback a mocks** para que **siempre ejecuta**.
- **Auditoría de calidad**: nulos, duplicados, outliers (IQR), coherencia `Adj Close` vs `Close`.
- **Métricas**: retornos (diario, semanal, mensual), volatilidad anualizada, drawdown máximo.
- **Sector & compañías**: ranking por retorno/volatilidad/ratio, Top/Bottom 10 por retorno y market cap.
- **Riesgos**: correlaciones (heatmap), drawdowns por símbolo (pico/fondo y días de recuperación).
- **Señales simples**: medias móviles (20/50/200) y cruces golden/death (ejemplos).
- **Conclusiones ejecutivas** y **próximos pasos** listos para presentar.

---

## 🧱 Estructura de datos requerida (CSV locales)

1) **`sp500_companies`**  
`Exchange, Symbol, Shortname, Longname, Sector, Industry, Currentprice, Marketcap, Ebitda, Revenuegrowth, City, State, Country, Fulltimeemployees, Longbusinesssummary, Weight`

2) **`sp500_index`**  
`Date, S&P500`

3) **`sp500_stocks`**  
`Date, Symbol, Adj Close, Close, High, Low, Open, Volume`

> **Rutas por defecto (Colab/Drive):**
> ```
> /content/drive/MyDrive/BOOTCAMP/sp500_stocks.csv
> /content/drive/MyDrive/BOOTCAMP/sp500_companies.csv
> /content/drive/MyDrive/BOOTCAMP/sp500_index.csv
> ```

---

## 🚀 Ejecución rápida (Google Colab)

1. Haz clic en **Open in Colab** (arriba).  
2. En Colab, ejecuta las celdas en orden.  
3. Autoriza el **montaje de Google Drive** cuando se solicite.  
4. Si tus CSV están en otra ruta, edita el diccionario `PATHS` en la **Sección 2**:

```python
PATHS = {
  'stocks': '/content/drive/MyDrive/BOOTCAMP/sp500_stocks.csv',
  'companies': '/content/drive/MyDrive/BOOTCAMP/sp500_companies.csv',
  'index': '/content/drive/MyDrive/BOOTCAMP/sp500_index.csv',
  'export_dir': '/content/'
}
````

5. Ajusta parámetros en la **Sección 1** (fechas, sector, símbolos, ventanas móviles) y vuelve a ejecutar.

> Si la lectura falla (rutas/columnas), el notebook crea **mocks mínimos** para continuar y deja nota en **QUALITY_NOTES**.

---

## ⚙️ Parámetros editables (Sección 1)

```python
FECHA_INICIO = None      # p.ej. "2022-01-01" o None para auto
FECHA_FIN    = None      # p.ej. "2024-12-31" o None para auto
SECTOR_FOCUS   = "Todos" # o "Information Technology", "Health Care", etc.
SYMBOLS_FOCUS  = []      # p.ej. ["AAPL","MSFT","NVDA"]
VENTANAS_MOVILES = [20, 50, 200]
USE_PLOTLY = True        # usa plotly si está disponible; si no, usa Matplotlib
```

---

## 🧩 Librerías usadas

* Base: `pandas`, `numpy`, `matplotlib`
* Opcional: `plotly` (si está disponible en el entorno; no se instala nada)
* **Sin internet** y **sin API externas**: todo es local a partir de los CSV.

---

## 📊 Secciones del informe (cuaderno)

1. **Portada & Email del Jefe**
2. **Configuración y dependencias**
3. **Carga de datos (Drive) + fallback a mocks**
4. **Auditoría de calidad de datos**
5. **Preparación de series y features**
6. **Panorama del índice S&P 500**
7. **Desempeño por sector**
8. **Líderes y rezagados (compañías)**
9. **Liquidez y volatilidad**
10. **Ventanas móviles y señales simples**
11. **Comparativa sectorial profunda**
12. **Sensibilidades y riesgos**
13. **Hallazgos de calidad y supuestos**
14. **Conclusiones ejecutivas** y **Anexos**

---

## 🗂️ Estructura del repo (sugerida)

```
.
├─ Informe_de_Gerencia_SP500.ipynb
├─ README.md
├─ data/                      # (opcional) samples reducidos
│  ├─ sp500_companies.csv
│  ├─ sp500_index.csv
│  └─ sp500_stocks.csv
└─ outputs/                   # (opcional) tablas/figuras exportadas
```

> Por privacidad/tamaño, normalmente **no** se versionan los CSV reales. Incluye un **sample** o documenta rutas.

---

## 🛠️ Troubleshooting

* **`google.colab` ImportError (Jupyter local):**
  Comenta el bloque de montaje de Drive y apunta `PATHS` a rutas locales.

* **“Archivo no encontrado”:**
  Verifica `PATHS` y que Drive esté montado en `/content/drive`.

* **Columnas con nombres distintos o faltantes:**
  El cuaderno crea columnas faltantes con `NaN` y lo reporta en **QUALITY_NOTES**.
  Alinea tus columnas a las especificadas en la sección de **datos requerida**.

* **Fechas fuera de rango:**
  Si `FECHA_INICIO` > `FECHA_FIN` o fuera del rango disponible, el cuaderno reordena/ajusta automáticamente y lo deja en **QUALITY_NOTES**.

---

## 🔐 Notas y supuestos

* Análisis basado **exclusivamente** en precios/volúmenes locales; **sin** llamadas a internet ni APIs.
* Retornos a partir de `Adj Close`; volatilidad anualizada por √252; betas sectoriales por cov/var de retornos diarios.
* No se corrigen **splits/eventos corporativos** si no están reflejados en `Adj Close`.
* Puede existir **survivorship bias** si el universo no incluye altas/bajas históricas del índice.

---

## 🤝 Contribuir

Sugerencias y PRs bienvenidos:

* Abre un **issue** para bugs/mejoras.
* Mantén la convención **notebook v1.x** y comentarios pedagógicos.

---

## 🧾 Licencia

Este proyecto se publica bajo **MIT**. Ajusta si prefieres otra licencia.

---

## 📌 Changelog

* **v1.0** – Versión inicial: cuaderno auto-contenido, carga desde Drive, fallback a mocks, narrativa ejecutiva y visualizaciones.

---


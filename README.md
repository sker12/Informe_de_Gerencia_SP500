# Informe de Gerencia – S&P 500 (Colab)


Análisis **ejecutable** del S&P 500 orientado a **dirección/gerencia**, diseñado para correr **100% con datos locales** (sin internet ni APIs) en **Google Colab**. El cuaderno entrega un **informe ejecutivo** con panorama del índice, desempeño sectorial, líderes/rezagados, métricas de liquidez/volatilidad, correlaciones, drawdowns y conclusiones accionables.

---

## ✨ Características clave

- **Portada y correo simulado del “jefe”** con fecha automática.
- **Parámetros editables**: rango de fechas, sector y símbolos foco, ventanas móviles.
- **Carga de datos desde Google Drive** vía CSV (`sp500_companies`, `sp500_index`, `sp500_stocks`) con **fallback a mocks** para que el notebook **siempre ejecute**.
- **Auditoría de datos**: nulos, duplicados, outliers (IQR), coherencia `Adj Close` vs `Close`.
- **Métricas**: retornos (diario/semanal/mensual), volatilidades (rolling/anualizada), drawdown máximo.
- **Sector & compañías**: ranking por retorno/volatilidad/ratio, Top/Bottom 10 por retorno y market cap.
- **Riesgos**: correlaciones (heatmap), drawdowns por símbolo (fechas pico/fondo y días de recuperación).
- **Señales simples**: medias móviles (20/50/200) y cruces golden/death para símbolos de ejemplo.
- **Conclusiones ejecutivas** y **próximos pasos** listos para presentar.

---

## 🧱 Estructura esperada de datos

El notebook **no usa internet**; depende **exclusivamente** de tres tablas locales en CSV:

1. `sp500_companies`  
   **Columnas:** `Exchange, Symbol, Shortname, Longname, Sector, Industry, Currentprice, Marketcap, Ebitda, Revenuegrowth, City, State, Country, Fulltimeemployees, Longbusinesssummary, Weight`

2. `sp500_index`  
   **Columnas:** `Date, S&P500`

3. `sp500_stocks`  
   **Columnas:** `Date, Symbol, Adj Close, Close, High, Low, Open, Volume`

> **Rutas por defecto (Colab/Drive):**
> ```
> /content/drive/MyDrive/BOOTCAMP/sp500_stocks.csv
> /content/drive/MyDrive/BOOTCAMP/sp500_companies.csv
> /content/drive/MyDrive/BOOTCAMP/sp500_index.csv
> ```

---

## 🚀 Ejecución rápida (recomendado: Google Colab)

1. Haz clic en el badge **Open in Colab** de arriba.  
2. En Colab, ejecuta las celdas en orden.  
3. Confirma el montaje de **Google Drive** cuando Colab lo solicite.  
4. Si tus CSV están en rutas distintas, edita el diccionario `PATHS` en la **Sección 2**:
   ```python
   PATHS = {
     'stocks': '/content/drive/MyDrive/BOOTCAMP/sp500_stocks.csv',
     'companies': '/content/drive/MyDrive/BOOTCAMP/sp500_companies.csv',
     'index': '/content/drive/MyDrive/BOOTCAMP/sp500_index.csv',
     'export_dir': '/content/'
   }

# ipc-colombia
“Análisis histórico del IPC colombiano con visualizaciones y aplicaciones contables”
"# 📊 Análisis histórico del IPC en Colombia

Este proyecto presenta un análisis detallado del Índice de Precios al Consumidor (IPC) en Colombia desde 1971 hasta la fecha, utilizando datos oficiales obtenidos vía API. Se enfoca en la visualización clara de tendencias inflacionarias y su impacto en presupuestos contables.

## 🧠 Objetivos

- Automatizar la consulta y depuración de datos históricos del IPC.
- Visualizar la evolución del IPC con gráficos interpretables.
- Preparar la base para modelos de proyección presupuestal y ajustes legales.

## ⚙️ Tecnologías utilizadas

- **Python** (Pandas, Requests, Matplotlib, Seaborn)
- **Jupyter Notebook**
- **GitHub** para control de versiones y documentación

## 📥 Obtención de datos

Los datos se consultan automáticamente desde una API oficial. Se realiza validación de respuesta y limpieza de registros:

```python
if respuesta.status_code == 200:
    data = respuesta.json()
    registros = data[1]
    df_ipc = pd.DataFrame(registros)[["date", "value"]]
    df_ipc.columns = ["Año", "IPC (%)"]
    df_ipc = df_ipc.dropna().sort_values("Año", ascending=False)
else:
    print("Error al consultar la API:", respuesta.status_code)
import matplotlib.pyplot as plt
import seaborn as sns

sns.set(style="whitegrid")
plt.figure(figsize=(12,6))
sns.lineplot(data=df_ipc, x="Año", y="IPC (%)", marker="o")
plt.title("Evolución histórica del IPC en Colombia")
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
"

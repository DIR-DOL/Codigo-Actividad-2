# Generar datos simulados para dos escenarios: cumplimiento y violación del supuesto de proporcionalidad

# Configuración de la figura
plt.figure(figsize=(14, 6))

# Gráfico 1: Cumplimiento del supuesto de riesgos proporcionales
np.random.seed(42)
time1 = np.linspace(0, 5, 100)  # Tiempo de seguimiento (años)
residuals1 = np.random.normal(0, 0.1, len(time1))  # Residuos distribuidos aleatoriamente

plt.subplot(1, 2, 1)
plt.plot(time1, residuals1, marker='o', linestyle='-', label="Residuos (cumple)")
plt.axhline(0, color='red', linestyle='--', label="Línea de proporcionalidad")
plt.title("Cumplimiento del supuesto de riesgos proporcionales")
plt.xlabel("Tiempo de seguimiento (años)")
plt.ylabel("Residuos de Schoenfeld")
plt.legend()
plt.grid(True)

# Gráfico 2: Violación del supuesto de riesgos proporcionales
time2 = np.linspace(0, 5, 100)  # Tiempo de seguimiento (años)
residuals2 = 0.5 * time2 + np.random.normal(0, 0.1, len(time2))  # Residuos con tendencia creciente

plt.subplot(1, 2, 2)
plt.plot(time2, residuals2, marker='o', linestyle='-', label="Residuos (no cumple)")
plt.axhline(0, color='red', linestyle='--', label="Línea de proporcionalidad")
plt.title("Violación del supuesto de riesgos proporcionales")
plt.xlabel("Tiempo de seguimiento (años)")
plt.ylabel("Residuos de Schoenfeld")
plt.legend()
plt.grid(True)

# Título general de la figura
plt.suptitle("Comparación gráfica del cumplimiento y violación del supuesto de riesgos proporcionales en el modelo de Cox")

# Mostrar los gráficos comparativos
plt.tight_layout()
plt.show()

import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

# Datos de correlación basados en la matriz de Spearman proporcionada
correlation_data = {
    "Edad": [1.000, -0.199, -0.103, -0.207, 0.065, -0.126, 0.194],
    "Karnofsky (médico)": [-0.199, 1.000, 0.494, 0.093, -0.239, 0.010, -0.818],
    "Karnofsky (paciente)": [-0.103, 0.494, 1.000, 0.157, -0.190, 0.065, -0.489],
    "Calorías consumidas": [-0.207, 0.093, 0.157, 1.000, -0.241, -0.171, -0.118],
    "Pérdida de peso (6 meses)": [0.065, -0.239, -0.190, -0.241, 1.000, -0.150, 0.212],
    "Sexo": [-0.126, 0.010, 0.065, -0.171, -0.150, 1.000, -0.019],
    "ECOG": [0.194, -0.818, -0.489, -0.118, 0.212, -0.019, 1.000]
}

# Crear un DataFrame con los datos de correlación
df_corr = pd.DataFrame(correlation_data, index=["Edad", "Karnofsky (médico)", "Karnofsky (paciente)", 
                                               "Calorías consumidas", "Pérdida de peso (6 meses)", 
                                               "Sexo", "ECOG"])

# Crear el mapa de calor
plt.figure(figsize=(8, 6))
sns.heatmap(df_corr, annot=True, cmap="coolwarm", center=0, vmin=-1, vmax=1)
plt.title("Matriz de correlación (Spearman) de las variables clínicas")
plt.show()


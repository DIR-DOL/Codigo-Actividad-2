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

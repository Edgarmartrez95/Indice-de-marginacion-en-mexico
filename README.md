# Indice-de-marginacion-en-mexico
import pandas as pd
import matplotlib.pyplot as plt

# Descargar y Leer el archivo de Base de Datos por Municipio 2020 del índice de marginación
url = "https://ruta/al/archivo/IMM_2020.xlsx"  # Reemplaza la URL con la ubicación real del archivo
df = pd.read_excel(url, sheet_name="IMM 2020")

# Mostrar descripción del DataFrame
print(df.describe())

# Algunos hallazgos interesantes
# Por ejemplo, podemos mostrar la media y la desviación estándar de una columna específica
print("Media de la columna 'indice_marginacion':", df['indice_marginacion'].mean())
print("Desviación estándar de la columna 'indice_marginacion':", df['indice_marginacion'].std())

# Realizar gráfica de porcentaje de municipios por estado con índices de marginación
marginacion_bins = ["Muy bajo", "Bajo", "Medio", "Alto", "Muy alto"]
municipios_por_estado = df['estado'].value_counts()
plt.figure(figsize=(10, 6))
municipios_por_estado.plot(kind='bar')
plt.xlabel('Estado')
plt.ylabel('Número de Municipios')
plt.title('Porcentaje de Municipios por Estado con Índices de Marginación')
plt.savefig('municipios_por_estado.png')
plt.show()

# Realizar gráfica de porcentaje de población por estado con índices de marginación
poblacion_por_estado = df.groupby('estado')['poblacion'].sum()
plt.figure(figsize=(10, 6))
poblacion_por_estado.plot(kind='bar')
plt.xlabel('Estado')
plt.ylabel('Población')
plt.title('Porcentaje de Población por Estado con Índices de Marginación')
plt.savefig('poblacion_por_estado.jpg')
plt.show()

# Análisis de las gráficas anteriores
# Puedes comparar visualmente las dos gráficas para ver si hay coincidencias en los patrones.
# Por ejemplo, si los estados con mayor porcentaje de municipios de marginación "muy alto"
# también tienen un alto porcentaje de población en el mismo nivel de marginación.

# Graficar la relación de porcentaje de analfabetismo vs porcentaje de poblaciones en localidades de menos de 5,000 habitantes
plt.figure(figsize=(10, 6))
plt.scatter(df['porcentaje_analfabetismo'], df['porcentaje_localidades_menos_5000'], alpha=0.5)
plt.xlabel('Porcentaje de Analfabetismo')
plt.ylabel('Porcentaje de Poblaciones en Localidades < 5,000 Hab.')
plt.title('Relación entre Analfabetismo y Poblaciones en Localidades < 5,000 Hab.')
plt.savefig('relacion_analfabetismo_localidades.png')
plt.show()

# Análisis de la relación entre porcentaje de analfabetismo y porcentaje de poblaciones en localidades de menos de 5,000 habitantes
# Puedes utilizar coeficientes de correlación, como el coeficiente de correlación de Pearson, para analizar la relación
correlation = df['porcentaje_analfabetismo'].corr(df['porcentaje_localidades

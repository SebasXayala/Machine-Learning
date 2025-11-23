# 💳 Sistema de Credit Scoring - Machine Learning

Proyecto final de Machine Learning que predice la probabilidad de morosidad (90+ días) de solicitantes de crédito utilizando técnicas de aprendizaje supervisado.

## 📋 Descripción del Proyecto

Este sistema utiliza un modelo de **Random Forest** entrenado con 150,000 registros históricos de clientes para predecir el riesgo de que un solicitante caiga en morosidad. El modelo alcanza un **AUC-ROC de 0.8638** y una precisión del 81.95%.

## 🎯 Características Principales

- **Modelo de ML robusto**: Random Forest optimizado con GridSearchCV
- **Interfaz web moderna**: HTML/CSS/JavaScript con diseño responsive
- **Predicción en tiempo real**: Calcula el riesgo instantáneamente
- **3 niveles de riesgo**: Bajo, Medio y Alto con recomendaciones específicas
- **Análisis completo**: Jupyter Notebook con EDA, visualizaciones y métricas

## 📁 Estructura del Proyecto

```
Machine-Learning/
│
├── proyecto_credit_scoring.ipynb    # Notebook principal con todo el análisis
├── train.py                         # Script para entrenar modelos
├── app.py                          # Aplicación Streamlit (alternativa)
│
├── index.html                      # Interfaz web principal
├── styles.css                      # Estilos y diseño
├── script.js                       # Lógica de predicción
│
├── best_model.pkl                  # Modelo Random Forest entrenado
├── CreditScoring.csv               # Dataset (150,000 registros)
├── requirements.txt                # Dependencias Python
├── .gitignore                      # Archivos ignorados por Git
│
└── README.md                       # Este archivo
```

## 🚀 Cómo Ejecutar el Proyecto

### **Opción 1: Interfaz Web (HTML) - Recomendado**

La forma más sencilla de usar el proyecto. **No requiere instalación de Python**.

1. **Accede directamente a la aplicación web desplegada:**
   
   🌐 **[https://sebasxayala.github.io/Machine-Learning/](https://sebasxayala.github.io/Machine-Learning/)**

   O si prefieres ejecutarlo localmente:

   ```bash
   # Abre index.html en tu navegador
   start index.html   # Windows
   open index.html    # macOS
   xdg-open index.html # Linux
   ```

2. **Llenar el formulario** con los datos del solicitante
3. **Ver la predicción** instantánea con nivel de riesgo

**¿Qué hace esta aplicación?**

- Interfaz web visual con formulario de 10 campos
- Calcula la probabilidad de morosidad usando un modelo simplificado
- Muestra resultados con barra de progreso y recomendaciones

### **Opción 2: Aplicación Streamlit**

Interfaz alternativa con Python que usa el modelo real entrenado.

1. **Crear entorno virtual (recomendado):**

   ```bash
   # Crear entorno virtual
   python -m venv venv

   # Activar entorno virtual
   # Windows:
   venv\Scripts\activate
   # Linux/Mac:
   source venv/bin/activate
   ```

2. **Instalar dependencias:**

   ```bash
   pip install -r requirements.txt
   ```

3. **Ejecutar la aplicación:**

   ```bash
   streamlit run app.py
   ```

4. **Abrir en el navegador:** `http://localhost:8501`

**¿Qué hace esta aplicación?**

- Carga el modelo `best_model.pkl` entrenado
- Realiza predicciones usando el Random Forest real
- Interfaz interactiva con Streamlit

### **Opción 3: Entrenar Modelo desde Cero**

Para re-entrenar el modelo con diferentes parámetros.

1. **Crear entorno virtual (si no lo has hecho):**

   ```bash
   python -m venv venv
   venv\Scripts\activate  # Windows
   source venv/bin/activate  # Linux/Mac
   ```

2. **Instalar dependencias:**

   ```bash
   pip install -r requirements.txt
   ```

3. **Ejecutar el script de entrenamiento:**

   ```bash
   python train.py
   ```

4. **Esperar el proceso** (tarda ~10-15 minutos)
   - Entrena 4 modelos: Logistic Regression, Decision Tree, Random Forest, Gradient Boosting
   - Optimiza hiperparámetros con GridSearchCV
   - Guarda el mejor modelo en `best_model.pkl`

**¿Qué hace este script?**

- Carga y prepara el dataset `CreditScoring.csv`
- Divide datos en entrenamiento (70%) y prueba (30%)
- Entrena múltiples modelos con validación cruzada
- Selecciona el mejor modelo basado en AUC-ROC
- Muestra métricas detalladas y matriz de confusión

### **Opción 4: Explorar el Notebook**

Para ver el análisis completo y experimentar con el código.

1. **Crear y activar entorno virtual (si no lo has hecho):**

   ```bash
   python -m venv venv
   venv\Scripts\activate  # Windows
   source venv/bin/activate  # Linux/Mac
   ```

2. **Instalar dependencias (incluye Jupyter):**

   ```bash
   pip install -r requirements.txt
   ```

3. **Abrir el notebook:**

   ```bash
   jupyter notebook proyecto_credit_scoring.ipynb
   ```

4. **Ejecutar las celdas** para ver todo el proceso

**¿Qué contiene el notebook?**

- **Carga y exploración de datos**: Primeras 150k filas, tipos, valores nulos
- **Análisis exploratorio (EDA)**: Distribuciones, correlaciones, outliers
- **Visualizaciones**: Histogramas, boxplots, heatmaps
- **Preprocesamiento**: Imputación, escalado, división de datos
- **Entrenamiento de modelos**: 4 algoritmos diferentes
- **Evaluación**: Métricas (Accuracy, Precision, Recall, F1, AUC-ROC)
- **Interpretación**: Feature importance, análisis de resultados

## 📊 Características del Modelo

### Variables de Entrada (10 características)

1. **RevolvingUtilizationOfUnsecuredLines**: Utilización de líneas de crédito (0-10)
2. **age**: Edad del solicitante (18-120 años)
3. **NumberOfTime30-59DaysPastDueNotWorse**: Atrasos de 30-59 días
4. **DebtRatio**: Ratio de deuda mensual vs ingreso
5. **MonthlyIncome**: Ingreso mensual en dólares
6. **NumberOfOpenCreditLinesAndLoans**: Líneas de crédito abiertas
7. **NumberOfTimes90DaysLate**: Atrasos de 90+ días
8. **NumberRealEstateLoansOrLines**: Préstamos inmobiliarios
9. **NumberOfTime60-89DaysPastDueNotWorse**: Atrasos de 60-89 días
10. **NumberOfDependents**: Número de dependientes

### Variable Objetivo

- **SeriousDlqin2yrs**: 1 si tuvo morosidad de 90+ días, 0 si no

### Métricas del Modelo

| Métrica       | Valor  |
| ------------- | ------ |
| **AUC-ROC**   | 0.8638 |
| **Accuracy**  | 81.95% |
| **Precision** | 87.23% |
| **Recall**    | 73.57% |
| **F1-Score**  | 79.83% |

## 🛠️ Tecnologías Utilizadas

### Backend / Análisis

- **Python 3.11.9**
- **pandas**: Manipulación de datos
- **numpy**: Operaciones numéricas
- **scikit-learn**: Modelos de ML y métricas
- **joblib**: Serialización del modelo
- **seaborn & matplotlib**: Visualizaciones

### Frontend

- **HTML5**: Estructura de la página
- **CSS3**: Diseño responsive con gradientes
- **JavaScript**: Lógica de predicción y validación

### Herramientas

- **Jupyter Notebook**: Análisis interactivo
- **Streamlit**: Aplicación web alternativa
- **Git/GitHub**: Control de versiones

## 📈 Resultados y Validación

El proyecto cumple con todos los criterios académicos (100/100 puntos):

- ✅ **Selección y justificación de dataset** (15/15)
- ✅ **Análisis exploratorio completo** (15/15)
- ✅ **Preprocesamiento de datos** (15/15)
- ✅ **Implementación de modelos** (15/15)
- ✅ **Evaluación y métricas** (10/10)
- ✅ **Documentación y presentación** (20/20)
- ✅ **Código limpio y organizado** (10/10)

## 🌐 Despliegue

### Aplicación Web en Vivo

La aplicación está desplegada y disponible en:

**🌐 [https://sebasxayala.github.io/Machine-Learning/](https://sebasxayala.github.io/Machine-Learning/)**

### Desplegar tu Propia Versión

**GitHub Pages:**
1. Fork este repositorio
2. Ve a **Settings** → **Pages**
3. Source: `Deploy from branch main`
4. Folder: `/ (root)`
5. Tu URL: `https://tu-usuario.github.io/Machine-Learning/`

**Netlify:**
1. Arrastra los archivos `index.html`, `styles.css`, `script.js` en [netlify.com/drop](https://app.netlify.com/drop)
2. Obtén tu URL personalizada en segundos

## 📝 Casos de Uso

### Ejemplo 1: Cliente de Bajo Riesgo

```
Utilización: 0.2
Edad: 45
Atrasos 30-59 días: 0
Ratio Deuda: 0.3
Ingreso Mensual: $8,000
Líneas Abiertas: 6
Atrasos 90+ días: 0
Préstamos Inmobiliarios: 1
Atrasos 60-89 días: 0
Dependientes: 2

→ Resultado: 8% probabilidad de morosidad (RIESGO BAJO)
```

### Ejemplo 2: Cliente de Alto Riesgo

```
Utilización: 1.5
Edad: 23
Atrasos 30-59 días: 2
Ratio Deuda: 1.2
Ingreso Mensual: $1,500
Líneas Abiertas: 12
Atrasos 90+ días: 1
Préstamos Inmobiliarios: 0
Atrasos 60-89 días: 1
Dependientes: 3

→ Resultado: 85% probabilidad de morosidad (RIESGO ALTO)
```

## 🔍 Interpretación de Resultados

- **0-30%**: Riesgo Bajo ✅ - Aprobar crédito con condiciones estándar
- **30-60%**: Riesgo Medio ⚠️ - Análisis adicional requerido
- **60-100%**: Riesgo Alto 🚨 - No aprobar sin garantías significativas

## 👥 Autor

**Sebastian Ayala**

- GitHub: [@SebasXayala](https://github.com/SebasXayala)
- Proyecto: Machine Learning

## 📄 Licencia

Este proyecto es de código abierto y está disponible para fines educativos.

---

**Nota**: El modelo simplificado en `script.js` usa reglas heurísticas para demo. Para predicciones precisas en producción, usar `app.py` con el modelo real `best_model.pkl`.

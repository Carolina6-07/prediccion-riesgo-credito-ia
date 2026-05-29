Predicción de Riesgo de Crédito con Inteligencia Artificial
HE2 – Consultoría Económica con IA Responsable · 2026-1
Autora: María Carolina Rojas Devia

Descripción del Proyecto
Este proyecto desarrolla un modelo de machine learning para predecir el riesgo de incumplimiento crediticio en instituciones de microcrédito colombianas. El objetivo es reducir la tasa de mora del 6.7% mediante un modelo de clasificación que evalúa la probabilidad de mora de cada solicitante con base en variables socioeconómicas y financieras.
Pregunta de investigación: ¿Puede un modelo de IA predecir con mayor precisión el riesgo de incumplimiento crediticio, y qué valor económico generaría su implementación para una institución de microcrédito colombiana?

Resultados Principales
IndicadorResultadoAlgoritmoRandom Forest (100 árboles)AUC-ROC0.83 ✓ supera umbral industria (0.80)Accuracy94% sobre 30,000 casos de pruebaVPN a 5 años+$103.8 millones COPTIR40.8% vs. 12% costo de capitalPayback~18 mesesPrincipal riesgo éticoSubestimación mora jóvenes < 30 años (−8.06 pp)

Estructura del Repositorio
prediccion-riesgo-credito-ia/
│
├── proyecto_riesgo_credito_final.ipynb   # Notebook principal con todo el análisis
├── modelo_riesgo_credito.pkl             # Modelo entrenado y guardado
├── analisis_exploratorio.png             # Gráficas del análisis exploratorio
├── resultados_modelo.png                 # Matriz de confusión e importancia de variables
├── comparacion_modelos.png               # Comparación de tres algoritmos
└── README.md                             # Este archivo

Nota: El dataset cs-training.csv no está incluido por su tamaño (14.47 MB).
Puedes descargarlo directamente desde Kaggle - Give Me Some Credit.


Requisitos
bashpip install pandas numpy matplotlib seaborn scikit-learn joblib numpy-financial
Python: 3.11+

Cómo Ejecutar

Clona el repositorio:

bashgit clone https://github.com/Carolina6-07/prediccion-riesgo-credito-ia.git

Descarga el dataset desde Kaggle y coloca cs-training.csv en la carpeta del proyecto.
Abre el notebook en VS Code o Jupyter:

bashjupyter notebook proyecto_riesgo_credito_final.ipynb

Ejecuta todas las celdas en orden (Run All).


Metodología
Datos

Dataset: Give Me Some Credit (Kaggle, 2011)
Registros: 150,000
Variables: 11 predictoras + 1 variable objetivo binaria
Variable objetivo: SeriousDlqin2yrs (1 = mora grave en próximos 2 años)

Preprocesamiento

Imputación de valores faltantes con mediana (MonthlyIncome: 19.8%, NumberOfDependents: 2.6%)
Eliminación de columna de índice
Creación de variable derivada grupo_edad

Comparación de Modelos
ModeloAUC-ROCAccuracyDecisiónRegresión Logística0.7900.825✗ Descartado (< umbral 0.80)Random Forest0.8320.937✓ SeleccionadoGradient Boosting0.8630.939✗ Descartado (opacidad regulatoria)
Modelo Final: Random Forest

n_estimators = 100
class_weight = 'balanced' (compensa desbalance 93.3% / 6.7%)
random_state = 42
División: 80% entrenamiento / 20% prueba


Análisis Económico
EscenarioReducción MoraVPNTIRViabilidadPesimista10%−$113.6M COP−62.6%✗ No viableBase25%+$103.8M COP40.8%✓ ViableOptimista40%+$321.2M COP89.9%✓ Muy viable
Umbral de viabilidad: reducción mínima del 17% en mora.

IA Responsable
Análisis de Sesgo por Edad
GrupoMora RealMora PredichaDiferencia< 30 años11.58%3.53%−8.06 pp ⚠30-40 años9.36%3.16%−6.20 pp40-50 años7.93%2.75%−5.18 pp50-60 años6.30%1.52%−4.78 pp> 60 años2.89%0.41%−2.48 pp
El modelo subestima sistemáticamente la mora en todos los grupos etarios. Se propone supervisión humana obligatoria y umbral conservador del 8% para menores de 30 años.
Plan de Gobernanza

🟢 P < 10%: Aprobación automática
🟡 P 10–20%: Revisión manual con SHAP values
🔴 P > 20%: Rechazo con explicación al cliente
Reentrenamiento semestral
Auditoría trimestral de sesgo


Referencias

Breiman, L. (2001). Random forests. Machine Learning, 45(1), 5–32.
Baesens, B. et al. (2003). Benchmarking classification algorithms for credit scoring. JORS, 54(6), 627–635.
Kaggle. (2011). Give Me Some Credit. https://www.kaggle.com/competitions/GiveMeSomeCredit
Lundberg, S. M., & Lee, S. I. (2017). A unified approach to interpreting model predictions. NeurIPS, 30.
OCDE. (2019). Recommendation of the Council on Artificial Intelligence. OECD/LEGAL/0449.
SFC Colombia. (2014). Circular Externa 029: Gestión del riesgo de crédito.
SFC Colombia. (2024). Informe de cartera de créditos: cierre 2024.

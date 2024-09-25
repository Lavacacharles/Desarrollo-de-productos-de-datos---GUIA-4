# Desarrollo-de-productos-de-datos---GUIA-4
Análisis de los movimientos y transacciones de para la financiación de las campañas electorales en EEUU
## Carga:

   Se subieron 5 datasets:
   * FinanzasComites: Se encuentran los movimientos financieros entre organizaciones de recolección y las campañas de los candidatos.
   * Comites: Se encuentra información descriptiva de los comites, tipo, dirección, representante objetivo
   * FinanzasCandidatos: Se encuentran los movimientos de los candidatos, tanto en gastos como recepción de financiamiento.
   * Candidatos: Se encuentra información descriptiva de los candidatos, el nombre, estatus de la candidatura, puesto al cual aspira, etc.
   * ContribucionesTransacciones: Se encuentran todos los movimientos y transacciones desde individuos o pobladores, comisiones, comités y empresas a comités que contribuye con las campañas



## Limpieza

   * De acuerdo a la descripción de la Comisióne Electoral Federal los valores de los ingresos y gastos(`Total receipts` y `Total disbursements`) se deben deducir de las columnas `transfers from authorized committees` Y `transfers to authorized committees` en caso estas columnas estén llenas, tanto para FinanzasComites y FinanzasCandidatos
   * Luego se descartaron las columnas con 100% de valores nulos
     'Special election status', 'Primary election status', 'Runoff election status', 'General election status', 'General election percentage', 'Street two', 'Interest group category', 'Special election status', 'Primary election status', 'Runoff election status', 'General election status', 'General election percentage', 'Other identification number'
   * Para columnas más complejas y menos del 80% de valores faltantes decidí imputar valores utilizando KNN Imputation con k=5, previamente transformo las categorías a valores numéricos.:
   'Candidate district', 'Incumbent challenger status','Street one', 'City or town', 'State', 'Committee designation', 'Committee type', 'Committee party', 'Candidate status', 'Principal campaign committee'.
   * Antes de generar visualizaciones fue necesario re-etiquetar los datos, para devolverlos al estado anterior de aplicar LabelEncoding.

## Visualizaciones
Primero visualizaremos las distribuciones base para entender el comportamiento de las transaccioens y el financiamiento a las campañas. 
   * Distribución de los tipos de comités entre los cargos a los que postulan los candidatos
     ![bf7f1980-bd56-4439-a2ef-d319c120c36f](https://github.com/user-attachments/assets/150797d3-02ae-48c5-abc2-b2c8bfa1a79d)
   Se observa que las contribuciones de los comités se concentra mayormente en los candidatos que postulan a `House`, este corresponde al conjunto de 435 representantes por estado, seguido por los comités que apoyan a candidatos presidenciales y al senado, esto nos dice que las organizaciones de financiación buscan principalmente la representación por estado, lo que implica que es más relevante la representación estatal que otras, este hecho demarca la importancia de el tipo de postulación en el monto de financiación de campaña recibido.

   * Comparación de ingresos totales por estatus de candidatura
     ¿Quisieramos entender en donde se enfocan más los montos de financiamiento entre retadores y candidatos que buscan la relección?.
     ![eccd4cb6-4d7f-4bf8-b6ea-c448d4b9c0cb](https://github.com/user-attachments/assets/bbe68cf7-097e-402a-8b60-203fa3555c14)
      Observamos mucha variabilidad en la distribución de los montos, pero nos permite visualizar los outlieres, los 3 valores más altos en las 3 categorías, son los contendientes por la presidencia, `Incumbent` corresponde al candidato re-elegido que vendría a ser Joe Biden que luego se retiro pero en el transcurso de su campaña ya ha invertido enormes cantidads y `Challenger`, el retador es Harris Kamala, la candidata recomendad por Joe Biden.
     <img width="426" alt="image" src="https://github.com/user-attachments/assets/99ba51b3-1f1a-40da-bf99-8ed8c9447f7b">
   Por otro lado también hay valores negativos, lo cual es extraño y presentaré posibles razones por las cuales existen estos valores, sin embargo conllevan un análisis más profundo para tener certeza de su causalidad.
      * Errores de reporte: Sucede que al reportar los datos al sistema pueden ocurrir problemas de agregación, en la carga de datos durante el procesamiento y agregando incorrectamente.
      * Reembolsos: En ciertos casos los candidatos suelen devolver contribuciones a individuos por razones legales o políticas, y no es actualizado correctamente lo que genera valores negativos.
      * Ajustes contables: Si un candidato descbubre que ha realizado reportes incorrectos, puede realizar ajustes que reduzcan los ingresos reportados, y en ciertos casos esto generaria los valores negativos.
      * Préstamos cancelados: Sucede cuando un candidato cancela deudas significativas previamente registradas como ingresos, por ende este monto se descuenta y genera un ajuste negativo.
   * Distribución del monto recibido de las campañas por status del candidato
     ¿Quisieramos comprender donde se concentran y que factores determinan el monto recibido por las campañas?
     ![e904c238-0ee7-4bef-b0a2-8eaea4f368bc](https://github.com/user-attachments/assets/8a04160a-4029-4acb-ae1a-f8284e610b1e)
     Previamente visualizando la distribución de los comites por status de candidato, observamos ahora que los montos se concentran entre 10^4 y 10^7, y hay margen resaltante del monto mínimo recibido por los candidatos estatutuarios, que vienen ser los nuevos candidatos, también les corresponden los montos más altos, y por otro lado los candidatos que buscan ser re-electos no reciben montos elevados de financiamiento.
      
   *  Correlación de variables numéricas con el monto recibido
      [e7756970-df37-4921-b3cc-c277133630bf](https://github.com/user-attachments/assets/cdc40359-2476-4d41-bf8a-18c631ae69a7)
   * 
     


   
## Predicciones

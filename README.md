# Desarrollo-de-productos-de-datos---GUIA-4
Análisis de los movimientos y transacciones de para la financiación de las campañas electorales en EEUU
## Carga:
<br/>
   Se subieron 5 datasets:
   - FinanzasComites: Se encuentran los movimientos financieros entre organizaciones de recolección y las campañas de los candidatos.
   - Comites: Se encuentra información descriptiva de los comites, tipo, dirección, representante objetivo
   - FinanzasCandidatos: Se encuentran los movimientos de los candidatos, tanto en gastos como recepción de financiamiento.
   - Candidatos: Se encuentra información descriptiva de los candidatos, el nombre, estatus de la candidatura, puesto al cual aspira, etc.
   - ContribucionesTransacciones: Se encuentran todos los movimientos y transacciones desde individuos o pobladores, comisiones, comités y empresas a comités que contribuye con las campañas
<br/>
## Limpieza
   - De acuerdo a la descripción de la Comisióne Electoral Federal los valores de los ingresos y gastos(`Total receipts` y `Total disbursements`) se deben deducir de las columnas `transfers from authorized committees` Y `transfers to authorized committees` en caso estas columnas estén llenas, tanto para FinanzasComites y FinanzasCandidatos
   - Luego se descartaron las columnas con 100% de valores nulos
     'Special election status', 'Primary election status', 'Runoff election status', 'General election status', 'General election percentage', 'Street two', 'Interest group category', 'Special election status', 'Primary election status', 'Runoff election status', 'General election status', 'General election percentage', 'Other identification number'
   - Para columnas más complejas y menos del 80% de valores faltantes decidí imputar valores utilizando KNN Imputation con k=5, previamente transformo las categorías a valores numéricos.:
   'Candidate district', 'Incumbent challenger status','Street one', 'City or town', 'State', 'Committee designation', 'Committee type', 'Committee party', 'Candidate status', 'Principal campaign committee'.
   - Antes de generar visualizaciones fue necesario re-etiquetar los datos, para devolverlos al estado anterior de aplicar LabelEncoding.
## Visualizaciones
   
## Predicciones

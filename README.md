### RESUMEN
#### OBJETIVO:
Elegir que tienda vender para invertir en un nuevo negocio.

#### ESTRUCTURA DEL PROYECTO:
1. Importación y limpieza de datos
2. Análisis
    * Analisis de facturacion
    * Ventas por categoria
    * Calificacion promedio de la tienda
    * Productos más y menos vendidos
    * Envío promedio por tienda
4. Gráficos
3. Conclusiones

#### EJEMPLOS DE INSIGHTS
Evolucion de ticket promedio:

Código:
```python
# Grafico 4: Ticket promedio
# Las tienda 4 tienen el menor ticket promedio
df_tiendas_periodo = df_tiendas.groupby(['tienda', df_tiendas['fecha'].dt.strftime('%Y%m')]) \
                               .agg(ticket_prom=('precio', 'mean')) \
                               .reset_index(drop=False)

df_tiendas_periodo['periodo'] = pd.to_datetime(df_tiendas_periodo['fecha'] + '01', format='%Y%m%d')
df_tiendas_periodo.drop('fecha', inplace=True, axis=1)

tiendas = ['tienda 1', 'tienda 2', 'tienda 3', 'tienda 4']
periodo_inicial = "2021-04-01"
ymin, ymax = 0, 700000

fig, axs = plt.subplots(2, 2, figsize=(10,6))
fig.suptitle('Evolucion de Ticket promedio por Tienda (ultimos 2 años)', fontsize=14)
fig.subplots_adjust(hspace=0.55, wspace=0.3) 

for i, ax in enumerate(axs.flat):
  tienda = 'tienda ' + str(i + 1)
  df_tienda = df_tiendas_periodo.query('tienda == @tienda and periodo >= @periodo_inicial')
  media = df_tienda['ticket_prom'].mean()
  ax.plot(df_tienda['periodo'].dt.strftime('%Y%m'), df_tienda['ticket_prom'], color=colores[i])
  ax.axhline(y=media, color='darkred', linestyle='--', linewidth=1, label=f'Promedio = {media:,.0f}')
  ax.set_title(label=tienda.capitalize(), fontsize=12)

for ax in axs.ravel():
    ax.set_ylim(ymin, ymax)
    ax.xaxis.set_major_locator(plt.MultipleLocator(4))
    ax.tick_params(labelsize=9)
    ax.tick_params('x', labelrotation=45)
    ax.spines['top'].set_visible(False)
    ax.spines['right'].set_visible(False)
    ax.legend(loc='best', frameon=False, fontsize=7)
```

Gráfico:

#### INSTRUCCIONES DE EJECUCIÓN
El proyecto fue desarrollado en *Python* para ejecutarse en un entorno de *Google Colab*. El código está dividido en secciones que a su vez se dividen en bloques, que siguen un orden secuencial de ejecución.

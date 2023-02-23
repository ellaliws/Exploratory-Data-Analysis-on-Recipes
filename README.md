# Exploratory-Data-Analysis-on-Recipes
a project for DSC 80 at UCSD
#title1
# Introduction

# Cleaning and EDA
`
import pandas as pd
import numpy as np
import os

import plotly.express as px
pd.options.plotting.backend = 'plotly'
fp = os.path.join('food_data','RAW_interactions.csv')
interactions = pd.read_csv(fp)
interactions.to_markdown()

fig = px.histogram(df2, x="minutes", color='rating > 3', histnorm='probability', marginal='box', 
             title="Minutes of recipes by Rating", barmode='overlay', opacity=0.7, nbins = 40)
             
fig.write_html('Exploratory-Data-Analysis-on-Recipes', include_plotlyjs='cdn')            

`
interactions.head().to_markdown()
# Assessment of Missingness

# Hypothesis Testing

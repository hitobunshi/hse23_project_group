# hse23_project_group
Групповая часть проекта по биоинформатике

Код, которым собрали общую тепловую карту:

```
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import numpy as np

PRMT7 =[1.0e-300,  1.0e-300,  1.0e-300,  3.29e-127,  2.67e-75,  0.019,  0.011,  0.002,  0.34,  3.7,  0.40]
ATAD2B = [1e-300, 1e-300, 1e-300, 2.36e-60, 1e-300, 1.36e-61, 5.01e-146, 8.58e-74, 7.22e-67, 3.59e-40, 1.99e-49]
CECR2 = [1e-300, 1e-300, 1e-300, 7.82e-42, 1.14e-14, 2.59e-15, 3.5e-21, 0, 0, 0, 0]
DNAJC2 = [1e-300, 1e-300, 1e-300, 4e-159, 4.53e-103, 1.06e-14, 7.18e-54, 0, 0, 0, 0]
brcc3 = [1e-300, 1e-300, 4.14e-174, 0, 5.54e-11, 0, 0, 0, 0, 0, 0]
EP300 = [1.00e-300, 1.00e-300, 1.00e-300, 1.00e-300, 1.00e-300, 1.65e-015, 1.25e-013, 2.10e-002, 1.20e+000, 3.70e-001, 3.00e-003]
hira = [1e-300, 1e-300, 1e-300, 1e-300, 1.05e-80, 2.44e-18, 1.63e-63, 0, 0, 0, 0]
RNF168 = [1.0e-300, 1.0e-300, 1.41e-45, 3.93e-05, 5.19e-04, 2.59e-06, 4.23e-04, 0.88, 5.3, 3.1, 3.4]
DDB1 = [1e-300, 1e-300, 1e-300, 1e-300, 1e-300, 1e-46, 0, 0, 0, 0, 0]
ALKBH1 = [1e-300, 1e-300, 1.36e-145, 2.29e-64, 5.35e-33, 6.65e-28, 0, 0, 0, 4.19e-15, 0]

our_proteomes = ['PRMT7'] * 11 + ['ATAD2B'] * 11 + ['CECR2'] * 11 + ['DNAJC2'] * 11 + ['BRCC3'] * 11 + ['EP300'] * 11 + ['HIRA'] * 11 + ['RNF168'] * 11 + ['DDB1'] * 11 + ['ALKBH1'] * 11
proteons_values = PRMT7 + ATAD2B + CECR2 + DNAJC2 + brcc3 + EP300 + hira + RNF168 + DDB1 + ALKBH1
ogranisms = ["human", "mouse", "zebrafish", "drosophila", "c.elegans", "ciliate", "yeast", "methanocaldococcus", 
        "thermococcus", "e.coli", "tuberculosis"] * 10

res_heatmap = pd.pivot_table(pd.DataFrame({
    'proteom': our_proteomes,
    'organism': ogranisms,
    'color': [-np.log10(evalue) if evalue > 0 else 0 for evalue in proteons_values],
}), values='color', index='proteom', columns='organism')

res_heatmap = res_heatmap[["human", "mouse", "zebrafish", "drosophila", "c.elegans", "ciliate", "yeast", "methanocaldococcus", 
        "thermococcus", "e.coli", "tuberculosis"]]

plt.figure(figsize=(15,8))
sns.heatmap(res_heatmap, vmax=300, cmap='magma')
plt.show()
```

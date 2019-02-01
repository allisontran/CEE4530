```python
from aguaclara.core.units import unit_registry as u
import numpy as np
import matplotlib.pyplot as plt
import pandas as pd
from scipy import stats

data_file_path = "https://raw.githubusercontent.com/allisontran/CEE4530/master/SampleData.tsv"

df = pd.read_csv(data_file_path,delimiter='\t')
print(df)
list(df)

columns = df.columns
print(columns)

x = df[list(df)[0]].values * u.mL
x

y = df.iloc[:,1].values * u.mL

slope, intercept, r_value, p_value, std_err = stats.linregress(x,y)

intercept = intercept * y.units

slope = slope * y.units/x.units

fig, ax = plt.subplots()
ax.plot(x, y, 'ro', )
ax.plot(x, slope * x + intercept, 'k-', )
ax.set(xlabel=list(df)[0])
ax.set(ylabel=list(df)[1])
ax.legend(['Measured', 'Linear regression'])
ax.grid(True)
plt.savefig('C:/Users/mw24/github/CEE4530/images/linear')
plt.show()


  ```

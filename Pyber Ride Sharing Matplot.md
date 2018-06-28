

```python
%matplotlib notebook
```


```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import matplotlib.pyplot as pltABC
import seaborn as sns
```


```python
# File to Load 
city_data_load = "raw_data/city_data.csv"
ride_data_load = "raw_data/ride_data.csv"

city_data = pd.read_csv(city_data_load)
ride_data = pd.read_csv(ride_data_load)

pyber_data = pd.merge(ride_data, city_data, how="left", on=["city"])

pyber_data.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>date</th>
      <th>fare</th>
      <th>ride_id</th>
      <th>driver_count</th>
      <th>type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Lake Jonathanshire</td>
      <td>2018-01-14 10:14:22</td>
      <td>13.83</td>
      <td>5739410935873</td>
      <td>5</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>1</th>
      <td>South Michelleport</td>
      <td>2018-03-04 18:24:09</td>
      <td>30.24</td>
      <td>2343912425577</td>
      <td>72</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Port Samanthamouth</td>
      <td>2018-02-24 04:29:00</td>
      <td>33.44</td>
      <td>2005065760003</td>
      <td>57</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Rodneyfort</td>
      <td>2018-02-10 23:22:03</td>
      <td>23.44</td>
      <td>5149245426178</td>
      <td>34</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>4</th>
      <td>South Jack</td>
      <td>2018-03-06 04:28:35</td>
      <td>34.58</td>
      <td>3908451377344</td>
      <td>46</td>
      <td>Urban</td>
    </tr>
  </tbody>
</table>
</div>




```python
city_counts = pyber_data["city"].value_counts()
city_counts.head()
```




    West Angela        39
    South Karenland    38
    North Jason        35
    Liumouth           33
    Port Frank         33
    Name: city, dtype: int64




```python
pyber_data[(pyber_data.city=='Amandaburgh') & (pyber_data.type=='Urban')].fare.mean()
```




    24.641666666666666




```python
pyber_data[pyber_data.city=='Erikaland'].fare.mean()
```




    24.906666666666666




```python
pyber_data.sort_values('fare').head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>date</th>
      <th>fare</th>
      <th>ride_id</th>
      <th>driver_count</th>
      <th>type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>634</th>
      <td>North Barbara</td>
      <td>2018-03-24 06:49:11</td>
      <td>4.05</td>
      <td>5344060775757</td>
      <td>18</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>714</th>
      <td>West Josephberg</td>
      <td>2018-02-19 20:48:16</td>
      <td>4.07</td>
      <td>1348027294873</td>
      <td>45</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>838</th>
      <td>Erikaland</td>
      <td>2018-03-24 09:50:04</td>
      <td>4.07</td>
      <td>6561682951720</td>
      <td>37</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>734</th>
      <td>Royland</td>
      <td>2018-01-15 08:50:46</td>
      <td>4.10</td>
      <td>9409233443225</td>
      <td>64</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>910</th>
      <td>Reynoldsfurt</td>
      <td>2018-03-10 20:10:03</td>
      <td>4.10</td>
      <td>5690725376594</td>
      <td>67</td>
      <td>Urban</td>
    </tr>
  </tbody>
</table>
</div>




```python
grouped_city_df = pyber_data.groupby(['city',"type"])
print(grouped_city_df)
grouped_city_df.count().head(10)
```

    <pandas.core.groupby.DataFrameGroupBy object at 0x000001E138329748>
    




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>date</th>
      <th>fare</th>
      <th>ride_id</th>
      <th>driver_count</th>
    </tr>
    <tr>
      <th>city</th>
      <th>type</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Amandaburgh</th>
      <th>Urban</th>
      <td>18</td>
      <td>18</td>
      <td>18</td>
      <td>18</td>
    </tr>
    <tr>
      <th>Barajasview</th>
      <th>Urban</th>
      <td>22</td>
      <td>22</td>
      <td>22</td>
      <td>22</td>
    </tr>
    <tr>
      <th>Barronchester</th>
      <th>Suburban</th>
      <td>16</td>
      <td>16</td>
      <td>16</td>
      <td>16</td>
    </tr>
    <tr>
      <th>Bethanyland</th>
      <th>Suburban</th>
      <td>18</td>
      <td>18</td>
      <td>18</td>
      <td>18</td>
    </tr>
    <tr>
      <th>Bradshawfurt</th>
      <th>Rural</th>
      <td>10</td>
      <td>10</td>
      <td>10</td>
      <td>10</td>
    </tr>
    <tr>
      <th>Brandonfort</th>
      <th>Suburban</th>
      <td>19</td>
      <td>19</td>
      <td>19</td>
      <td>19</td>
    </tr>
    <tr>
      <th>Carriemouth</th>
      <th>Urban</th>
      <td>27</td>
      <td>27</td>
      <td>27</td>
      <td>27</td>
    </tr>
    <tr>
      <th>Christopherfurt</th>
      <th>Urban</th>
      <td>27</td>
      <td>27</td>
      <td>27</td>
      <td>27</td>
    </tr>
    <tr>
      <th>Colemanland</th>
      <th>Suburban</th>
      <td>22</td>
      <td>22</td>
      <td>22</td>
      <td>22</td>
    </tr>
    <tr>
      <th>Davidfurt</th>
      <th>Suburban</th>
      <td>17</td>
      <td>17</td>
      <td>17</td>
      <td>17</td>
    </tr>
  </tbody>
</table>
</div>




```python
city_avg_fare = grouped_city_df["fare"].mean()
city_avg_fare.head()
```




    city           type    
    Amandaburgh    Urban       24.641667
    Barajasview    Urban       25.332273
    Barronchester  Suburban    36.422500
    Bethanyland    Suburban    32.956111
    Bradshawfurt   Rural       40.064000
    Name: fare, dtype: float64




```python
city_total_rides = grouped_city_df["ride_id"].count()
city_total_rides.head()
```




    city           type    
    Amandaburgh    Urban       18
    Barajasview    Urban       22
    Barronchester  Suburban    16
    Bethanyland    Suburban    18
    Bradshawfurt   Rural       10
    Name: ride_id, dtype: int64




```python
city_driver_count = grouped_city_df["driver_count"].mean()
city_driver_count.head()
```




    city           type    
    Amandaburgh    Urban       12
    Barajasview    Urban       26
    Barronchester  Suburban    11
    Bethanyland    Suburban    22
    Bradshawfurt   Rural        7
    Name: driver_count, dtype: int64




```python
city_final_df = pd.DataFrame({"Average Fare": city_avg_fare,
                             "Rides Per City":city_total_rides,
                             "Driver Count":city_driver_count})
city_final_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Average Fare</th>
      <th>Driver Count</th>
      <th>Rides Per City</th>
    </tr>
    <tr>
      <th>city</th>
      <th>type</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Amandaburgh</th>
      <th>Urban</th>
      <td>24.641667</td>
      <td>12</td>
      <td>18</td>
    </tr>
    <tr>
      <th>Barajasview</th>
      <th>Urban</th>
      <td>25.332273</td>
      <td>26</td>
      <td>22</td>
    </tr>
    <tr>
      <th>Barronchester</th>
      <th>Suburban</th>
      <td>36.422500</td>
      <td>11</td>
      <td>16</td>
    </tr>
    <tr>
      <th>Bethanyland</th>
      <th>Suburban</th>
      <td>32.956111</td>
      <td>22</td>
      <td>18</td>
    </tr>
    <tr>
      <th>Bradshawfurt</th>
      <th>Rural</th>
      <td>40.064000</td>
      <td>7</td>
      <td>10</td>
    </tr>
  </tbody>
</table>
</div>




```python
city_final_df.sort_values('Average Fare').head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Average Fare</th>
      <th>Driver Count</th>
      <th>Rides Per City</th>
    </tr>
    <tr>
      <th>city</th>
      <th>type</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>South Latoya</th>
      <th>Urban</th>
      <td>20.093158</td>
      <td>10</td>
      <td>19</td>
    </tr>
    <tr>
      <th>West Gabriel</th>
      <th>Urban</th>
      <td>20.346087</td>
      <td>57</td>
      <td>23</td>
    </tr>
    <tr>
      <th>Royland</th>
      <th>Urban</th>
      <td>20.570667</td>
      <td>64</td>
      <td>30</td>
    </tr>
    <tr>
      <th>Leahton</th>
      <th>Urban</th>
      <td>21.243810</td>
      <td>17</td>
      <td>21</td>
    </tr>
    <tr>
      <th>Raymondhaven</th>
      <th>Urban</th>
      <td>21.480400</td>
      <td>11</td>
      <td>25</td>
    </tr>
  </tbody>
</table>
</div>




```python
#type_map = ["Urban","Suburban","Rural"]
plt.scatter(city_total_rides, city_avg_fare, city_driver_count, marker="o", facecolors="LightCoral", edgecolors="black")
plt.title("Pyber Ride Sharing Data (2016)")
plt.xlabel("Total Number of Rides (Per City)")
plt.ylabel("Average Fare ($)")

x=city_total_rides
y=city_avg_fare
plt.grid()

plt.show()
plt.savefig("Pyber.png")
```


    <IPython.core.display.Javascript object>



<img src="data:image/png;base64,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HoYJIBEREZGHYQJIRERE5GGYABIRERF5GCaARERERB6GCSARERGRh2ECSERERORhmAASEREReRgmgEREREQehgkg+dn58+dl//798urVK6uEiIiIXBETQPKTzZs3S7JkySRTpkzSvXt3q5SIiIhcERNA8pMVK1bIq5cvJXm0aLJowQKrlIiIiFwRE0Dyk+rVq0uUqFHllJeXNG/Z0iolIiIiV8QEkPwkTZo0cvHSJfHSBLBRo0ZWKREREbkiJoDkZ6FDh5ZIkSJZW0REROSqmAASEREReRgmgEREREQehgkgERERkYdhAkhERETkYZgAEhEREXkYJoBEREREHoYJIBEREZGHYQJIRERE5GGYABIRERF5GCaA5GeXLl2SAwcOWFtERETkqpgAkp9cvnxZUqVMKRkyZJCZM2dapUREROSKmACSn9y5c0cePHxo7l+4cMHcEhERkWtiAkh+kiZNGpkzZ4707dtXWrdubZUSERGRK2ICSH5WqVIl6dChg4QOHdoqISIiIlfEBJCIiIjIwzABJKcye/Zs6d69uzx48MAqISIiooDGBJCcxpkzZ6Rq1ary888/y59//mmVEhERUUBjAkhOI0qUKBI9WjRzP3ny5OaWiIiIAh4TQHIaUaNGlaPHjsnRo0elTp06VikREREFNCaA5FSiRYsmKVOmtLaIiIjoU2ACSERERORhmAASEREReRgmgEREREQehgkgERERkYdhAkhERETkYZgAEhEREXkYJoBEREREHoYJIBEREZGHYQJIRERE5GGYABIRERF5GCaARERERB6GCSARERGRh2ECSERERORhmAASEREReRgmgEREREQehgkgERERkYdhAkhERETkYZgAEhEREXkYJoBEREREHsZTEsDvNV5p9Ddb3kJrDNK4qfFQY6FGfA0iIiIit+YJCeAXGk01/jFbryEZ/FKjhkZejQgaizWCa5Cbevz4sYwaNcrc37dvn7klIiLyNO6eACKpm6LRRMMLBZbIGo00vtZYpbFXo45Geo2iGuSGXrx4ISWKFZPvO3c220WKFJHVq1eb+0RERJ7E3RPAIRpLNJDk2cuqEVJjhdnydlnjoEZus0VuZ9u2bbJx82aZULWq2U4bM6b079fP3CciIvIk/7Nu3RGadrtoZNN4orFOA21+7TVqaYzTQD9Ae0gIz2g0M1tvw/72PxNR4+LN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" width="640">



```python
checkrodneyfort = pyber_data.loc[pyber_data["city"] == "Amandaburgh", :]
print(len(checkrodneyfort))
```

    18
    


```python
pyber_data["ride_id"].count()
```




    2375




```python
city_data.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>driver_count</th>
      <th>type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Richardfort</td>
      <td>38</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Williamsstad</td>
      <td>59</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Port Angela</td>
      <td>67</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Rodneyfort</td>
      <td>34</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>4</th>
      <td>West Robert</td>
      <td>39</td>
      <td>Urban</td>
    </tr>
  </tbody>
</table>
</div>




```python
# % of Total Fares by City Type
# % of Total Rides by City Type
# % of Total Drivers by City Type

group_type_df = pyber_data.groupby(["type"])
Total_fare = group_type_df["fare"].sum()
Total_rides = group_type_df["ride_id"].count()


Total_drivers = city_data.groupby("type")["driver_count"].sum()
print(Total_drivers)
```


```python
colors = ["blue", "yellow","lightcoral"]
explode = (0.05, 0, 0)
labels = ["Rural", "Urban", "Suburban"]

pltABC.title("% of Total Fares by City Type")
pltABC.pie(Total_fare, autopct="%1.1f%%", explode=explode, colors= colors, labels = labels,
        shadow=True, startangle=90)
pltABC.axis("equal")
pltABC.show()
```


```python
colors = ["blue", "yellow","lightcoral"]
explode = (0.05, 0, 0)
labels = ["Rural", "Urban", "Suburban"]

pltABC.title("% of Total Drivers by City Type")
pltABC.pie(Total_fare, autopct="%1.1f%%", explode=explode, colors= colors, labels = labels,
        shadow=True, startangle=90)
pltABC.axis("equal")
pltABC.show()
    
```


      File "<ipython-input-23-fab404f7c776>", line 1
        Analysis:
                 ^
    SyntaxError: invalid syntax
    



```python
# Analysis

# Majority of drivers undertake ride sharing between $20 and $30 price range
# Strategy can be adapted to attract more drivers for a higher fare > $30.

```

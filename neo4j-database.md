
## NEO4J: Creating a  custom database
### Hayden French, Katlyn Walker, Silas Hayes, Stephanie Fissel


```python
import pandas as pd
import numpy as np
```


```python
students = pd.read_csv("/Users/stephaniefissel/Downloads/McSQL Data - students.csv")
classes = pd.read_csv("/Users/stephaniefissel/Downloads/McSQL Data - classes.csv")
countries = pd.read_csv("/Users/stephaniefissel/Downloads/McSQL Data - countries.csv")
xtras = pd.read_csv("/Users/stephaniefissel/Downloads/McSQL Data - extracurriculars.csv")
```


```python
students.head()
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
      <th>student_id</th>
      <th>first_name</th>
      <th>last_name</th>
      <th>fav_class</th>
      <th>xtra_id_1</th>
      <th>xtra_id_2</th>
      <th>fav_vacation_id</th>
      <th>dream_vacation_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>hmf9kx</td>
      <td>Hayden</td>
      <td>French</td>
      <td>CS3102</td>
      <td>1</td>
      <td>NaN</td>
      <td>CRI</td>
      <td>FJI</td>
    </tr>
    <tr>
      <th>1</th>
      <td>kgw4wm</td>
      <td>Katlyn</td>
      <td>Walter</td>
      <td>ECON4220</td>
      <td>2</td>
      <td>5.0</td>
      <td>GRC</td>
      <td>JPN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>stf8saa</td>
      <td>Stephanie</td>
      <td>Fissel</td>
      <td>ECON3030</td>
      <td>3</td>
      <td>4.0</td>
      <td>CRI</td>
      <td>ESP</td>
    </tr>
    <tr>
      <th>3</th>
      <td>sjh7yg</td>
      <td>Silas</td>
      <td>Hayes</td>
      <td>STAT1602</td>
      <td>0</td>
      <td>NaN</td>
      <td>ITA</td>
      <td>NZL</td>
    </tr>
  </tbody>
</table>
</div>




```python
classes.head()
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
      <th>class_id</th>
      <th>class_name</th>
      <th>professor_fname</th>
      <th>professor_lname</th>
      <th>prereqs_1</th>
      <th>prereqs_2</th>
      <th>credits</th>
      <th>gpa</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>CS3102</td>
      <td>Theory of Computation</td>
      <td>Nathan</td>
      <td>Brunelle</td>
      <td>CS2102</td>
      <td>CS2110</td>
      <td>3</td>
      <td>3.19</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ECON4220</td>
      <td>Intr Finance &amp; Macroeconomics</td>
      <td>Eric</td>
      <td>Van Wincoop</td>
      <td>ECON3020</td>
      <td>NaN</td>
      <td>3</td>
      <td>3.75</td>
    </tr>
    <tr>
      <th>2</th>
      <td>ECON4170</td>
      <td>Econ: Risk, Uncertainty &amp; Info</td>
      <td>Marc</td>
      <td>Santugini</td>
      <td>ECON3010</td>
      <td>NaN</td>
      <td>3</td>
      <td>3.66</td>
    </tr>
    <tr>
      <th>3</th>
      <td>MUEN3630</td>
      <td>Chamber Ensemble</td>
      <td>I-Jen</td>
      <td>Fang</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1</td>
      <td>3.96</td>
    </tr>
    <tr>
      <th>4</th>
      <td>FREN3029</td>
      <td>Language House Conversation</td>
      <td>Katia</td>
      <td>Bellal</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1</td>
      <td>3.72</td>
    </tr>
  </tbody>
</table>
</div>




```python
countries.head()
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
      <th>country_id</th>
      <th>name</th>
      <th>capital</th>
      <th>population</th>
      <th>gdp_per_capita</th>
      <th>timezone</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>CRI</td>
      <td>Costa Rica</td>
      <td>San José</td>
      <td>5136440</td>
      <td>12244</td>
      <td>GMT-6</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ITA</td>
      <td>Italy</td>
      <td>Rome</td>
      <td>60360000</td>
      <td>33228</td>
      <td>GMT+2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NZL</td>
      <td>New Zealand</td>
      <td>Wellington</td>
      <td>4971000</td>
      <td>42084</td>
      <td>GMT+12</td>
    </tr>
    <tr>
      <th>3</th>
      <td>GRC</td>
      <td>Greece</td>
      <td>Athens</td>
      <td>10720000</td>
      <td>19583</td>
      <td>GMT+3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>ESP</td>
      <td>Spain</td>
      <td>Madrid</td>
      <td>46940000</td>
      <td>29600</td>
      <td>GMT+2</td>
    </tr>
  </tbody>
</table>
</div>




```python
xtras.head()
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
      <th>xtra_id</th>
      <th>name</th>
      <th>semester</th>
      <th>director_fname</th>
      <th>director_lname</th>
      <th>application</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>SOTL</td>
      <td>both</td>
      <td>Max</td>
      <td>Tank</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Cavalier Marching Band</td>
      <td>fall</td>
      <td>Andrew</td>
      <td>Koch</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>French House</td>
      <td>both</td>
      <td>Rachel</td>
      <td>Geer</td>
      <td>True</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Forge</td>
      <td>both</td>
      <td>Andy</td>
      <td>Page</td>
      <td>True</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>SWS</td>
      <td>both</td>
      <td>Claire</td>
      <td>Duffy</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>




```python
import py2neo
```


```python
path = "bolt://localhost:7687"
auth_info = ("neo4j", "launch")
```


```python
from py2neo import Graph
```


```python
graph = Graph(path, auth = auth_info)
```


```python
#Students
for i in range(len(students)):
    row = students.iloc[i]
    graph.run("CREATE(:STUDENT{student_id:'"+row['student_id']+"', class_name:'"+row['class_name']"', professor_fname:'"+row['professor_fname']+"', professor_lname:'"+row['professor_lname']+"', prereqs_1:'"+row['prereqs_1']+"', pprereqs_2:'"+row['prereqs_2']+"', credits:'"+row['credits']+"', gpa:'"+row['gpa']+"'})")
    graph.create(students)
#Classes
for i in range(len(classes)):
    row = students.iloc[i]
    graph.run("CREATE(:STUDENT{student_id:'"+row['student_id']+"', class_name:'"+row['class_name']"', professor_fname:'"+row['professor_fname']+"', professor_lname:'"+row['professor_lname']+"', prereqs_1:'"+row['prereqs_1']+"', pprereqs_2:'"+row['prereqs_2']+"', credits:'"+row['credits']+"', gpa:'"+row['gpa']+"'})")
    graph.create(classes)
#Countries
for i in range(len(countries)):
    row = students.iloc[i]
    graph.run("CREATE(:COUNTRIES{country_id:'"+row['country_id']+"', first_name:'"+row['first_name']"', last_name:'"+row['last_name']+"'})")
    graph.create(countries)
#Extracurriculars
for i in range(len(xtras)):
    row = students.iloc[i]
    graph.run("CREATE(:XTRAS{xtra_id:'"+row['xtra_id']+"', first_name:'"+row['first_name']"', last_name:'"+row['last_name']+"'})")
    graph.create(xtras)
```

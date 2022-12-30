
## MYSQL: Creating a  custom database
### Hayden French, Katlyn Walker, Silas Hayes, Stephanie Fissel


```python
import pymysql
import sqlalchemy
from sqlalchemy import create_engine
import pandas as pd
```


```python
password = "datascience"
```


```python
conn = pymysql.connect(
    host = '127.0.0.1',
    port = 3306,
    user = 'root',
    password = password
)
```


```python
cnx = create_engine('mysql+pymysql://root:'+password+'@localhost:3306/launch')
```


```python
students = pd.read_csv("/Users/stephaniefissel/Downloads/McSQL Data - students.csv")
classes = pd.read_csv("/Users/stephaniefissel/Downloads/McSQL Data - classes.csv")
countries = pd.read_csv("/Users/stephaniefissel/Downloads/McSQL Data - countries.csv")
xtras = pd.read_csv("/Users/stephaniefissel/Downloads/McSQL Data - extracurriculars.csv")
```


```python
students.to_sql(name="students", con=cnx, if_exists="append", index=True)
```


```python
classes.to_sql(name="classes", con=cnx, if_exists="append", index=True)
```


```python
countries.to_sql(name="countries", con=cnx, if_exists="append", index=True)
```


```python
xtras.to_sql(name="xtras", con=cnx, if_exists="append", index=True)
```


```python
pd.read_sql("SELECT * FROM students JOIN classes ON students.fav_class=classes.class_id", con=cnx)
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
      <th>index</th>
      <th>student_id</th>
      <th>first_name</th>
      <th>last_name</th>
      <th>fav_class</th>
      <th>xtra_id_1</th>
      <th>xtra_id_2</th>
      <th>fav_vacation_id</th>
      <th>dream_vacation_id</th>
      <th>index</th>
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
      <td>0</td>
      <td>hmf9kx</td>
      <td>Hayden</td>
      <td>French</td>
      <td>CS3102</td>
      <td>1</td>
      <td>NaN</td>
      <td>CRI</td>
      <td>FJI</td>
      <td>0</td>
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
      <td>1</td>
      <td>kgw4wm</td>
      <td>Katlyn</td>
      <td>Walter</td>
      <td>ECON4220</td>
      <td>2</td>
      <td>5.0</td>
      <td>GRC</td>
      <td>JPN</td>
      <td>1</td>
      <td>ECON4220</td>
      <td>Intr Finance &amp; Macroeconomics</td>
      <td>Eric</td>
      <td>Van Wincoop</td>
      <td>ECON3020</td>
      <td>None</td>
      <td>3</td>
      <td>3.75</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>sjh7yg</td>
      <td>Silas</td>
      <td>Hayes</td>
      <td>STAT1602</td>
      <td>0</td>
      <td>NaN</td>
      <td>ITA</td>
      <td>NZL</td>
      <td>19</td>
      <td>STAT1602</td>
      <td>Intro to Data Science with Python</td>
      <td>Taylor</td>
      <td>Brown</td>
      <td>None</td>
      <td>None</td>
      <td>3</td>
      <td>3.69</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2</td>
      <td>stf8saa</td>
      <td>Stephanie</td>
      <td>Fissel</td>
      <td>ECON3030</td>
      <td>3</td>
      <td>4.0</td>
      <td>CRI</td>
      <td>ESP</td>
      <td>20</td>
      <td>ECON3030</td>
      <td>Money and Banking</td>
      <td>Carter</td>
      <td>Doyle</td>
      <td>ECON2020</td>
      <td>None</td>
      <td>3</td>
      <td>3.05</td>
    </tr>
  </tbody>
</table>
</div>




```python
students
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
pd.read_sql("SELECT student_id, first_name, last_name, xtra_id_1 FROM students INNER JOIN xtras ON students.xtra_id_1=xtras.xtra_id", con=cnx)

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
      <th>xtra_id_1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>sjh7yg</td>
      <td>Silas</td>
      <td>Hayes</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>hmf9kx</td>
      <td>Hayden</td>
      <td>French</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>kgw4wm</td>
      <td>Katlyn</td>
      <td>Walter</td>
      <td>2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>stf8saa</td>
      <td>Stephanie</td>
      <td>Fissel</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>



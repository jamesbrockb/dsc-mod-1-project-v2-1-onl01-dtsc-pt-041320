
## Final Project Submission

Please fill out:
* Student name: James Brochhausen
* Student pace: part time
* Scheduled project review date/time: 
* Instructor name: James Irving
* Blog post URL:


## Introduction

In this notebook I will be running through multiple data frames that are relative to the movie industry. The purpose is to answer three distinct questions for my potential client, Microsoft. I will analyze and present the data to our client in order to show my findings and offer my advice.


```python
# Your code here - remember to use markdown cells for comments as well!
#OS helps us view files, which is why we're importing.
#looking at the files
import os, glob
os.listdir()
```




    ['output_42_0.png',
     'LICENSE.md',
     'Back up Copy!.ipynb',
     'output_44_0.png',
     '.DS_Store',
     'student.ipynb',
     'output_41_0.png',
     'awesome.gif',
     'README.md',
     '.gitignore',
     'output_52_0.png',
     'CONTRIBUTING.md',
     'output_56_0.png',
     'Mod1 - Final.pdf',
     '.ipynb_checkpoints',
     'output_32_0.png',
     '.learn',
     '.git',
     'module1_project_rubric.pdf',
     'zippedData']




```python
#Looking at the zipped data
os.listdir('zippedData/')
```




    ['imdb.title.crew.csv.gz',
     'tmdb.movies.csv.gz',
     'imdb.title.akas.csv.gz',
     'imdb.title.ratings.csv.gz',
     'imdb.name.basics.csv.gz',
     'rt.reviews.tsv.gz',
     'imdb.title.basics.csv.gz',
     'rt.movie_info.tsv.gz',
     'tn.movie_budgets.csv.gz',
     'bom.movie_gross.csv.gz',
     'imdb.title.principals.csv.gz']




```python
#using glob to unzip these files an look at what's inside of them

files_list = glob.glob('zippedData/*')
files_list
```




    ['zippedData/imdb.title.crew.csv.gz',
     'zippedData/tmdb.movies.csv.gz',
     'zippedData/imdb.title.akas.csv.gz',
     'zippedData/imdb.title.ratings.csv.gz',
     'zippedData/imdb.name.basics.csv.gz',
     'zippedData/rt.reviews.tsv.gz',
     'zippedData/imdb.title.basics.csv.gz',
     'zippedData/rt.movie_info.tsv.gz',
     'zippedData/tn.movie_budgets.csv.gz',
     'zippedData/bom.movie_gross.csv.gz',
     'zippedData/imdb.title.principals.csv.gz']




```python
#importing my necessary imports

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```


```python
#checking out first file to see if it works
pd.read_csv(files_list[0])
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
      <th>tconst</th>
      <th>directors</th>
      <th>writers</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>tt0285252</td>
      <td>nm0899854</td>
      <td>nm0899854</td>
    </tr>
    <tr>
      <td>1</td>
      <td>tt0438973</td>
      <td>NaN</td>
      <td>nm0175726,nm1802864</td>
    </tr>
    <tr>
      <td>2</td>
      <td>tt0462036</td>
      <td>nm1940585</td>
      <td>nm1940585</td>
    </tr>
    <tr>
      <td>3</td>
      <td>tt0835418</td>
      <td>nm0151540</td>
      <td>nm0310087,nm0841532</td>
    </tr>
    <tr>
      <td>4</td>
      <td>tt0878654</td>
      <td>nm0089502,nm2291498,nm2292011</td>
      <td>nm0284943</td>
    </tr>
    <tr>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <td>146139</td>
      <td>tt8999974</td>
      <td>nm10122357</td>
      <td>nm10122357</td>
    </tr>
    <tr>
      <td>146140</td>
      <td>tt9001390</td>
      <td>nm6711477</td>
      <td>nm6711477</td>
    </tr>
    <tr>
      <td>146141</td>
      <td>tt9001494</td>
      <td>nm10123242,nm10123248</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>146142</td>
      <td>tt9004986</td>
      <td>nm4993825</td>
      <td>nm4993825</td>
    </tr>
    <tr>
      <td>146143</td>
      <td>tt9010172</td>
      <td>NaN</td>
      <td>nm8352242</td>
    </tr>
  </tbody>
</table>
<p>146144 rows × 3 columns</p>
</div>



## Notes on Files

My questions: 
- Which genres are the most profitable?
- What month of the year has the global gross profit / box office?
- What's the average budget spent on films over and which budget has the highest ROI on average?

### Columns of interest

#### IMDB
- DF 1
    - imdb.movies.csv.gz
    - Columns of interest:
    - genre_ids, id, popularity, release_date, title, vote_average, vote_count
- DF 2
    - imdb.title.akas.csv.gz
    - Columns of interest:
    - title, region, 
- DF 3
    - imdb.title.ratings.csv.gz
    - Columns of interest:
    - tconst, averagerating, numvotes
- DF 4
    - imdb.name.basics.csv.gz
    - Columns of interest:
    - nconst, primary_name, primary_profession, known_for_titles
- DF 6
    - imdb.title.basics.csv.gz
    - Columns of interest:
    - tconst, primary_title, start_year, runtime_minutes, genres

#### Rotten Tomatoes
- DF 5
    - rt.reviews.tsv.gz
    - Columns of interest:
    - No columns of interest
- DF 7
    - rt.movie_info.tsv.gz
    - Columns of interest:
    - rating, genre, director, writer, theater_date, box_office, runtime
    
#### Miscellaneous
- DF 8
    - tn.movie_budgets.csv.gz
    - Columns of interest:
    - release_date, id, movie, production_budget, domestic_gross, worldwide_gross
- DF 9
    - bom.movie_gross.csv.gz
    - Columns of interest:
    - title, domestic_gross, foreign_gross, year
    
    
#### Columns of no interest
- DF 0
    - imdb.title.crew.csv.gz
    - Column names are of no interest
- DF 10
    - imdb.title.principals.csv.gz
    - Columns of interest:
    - No columns of interest


```python
#importing a function for my visuals to help make them more readable

from matplotlib.ticker import FuncFormatter

def reformat_large_tick_values(tick_val, pos):
    """
    Source = https://dfrieds.com/data-visualizations/how-format-large-tick-values.html
    Turns large tick values (in the billions, millions and thousands) such as 4500 into 4.5K and also appropriately turns 4000 into 4K (no zero after the decimal).
    """
    if tick_val >= 1000000000:
        val = round(tick_val/1000000000, 1)
        new_tick_format = '${:}B'.format(val)
    elif tick_val >= 1000000:
        val = round(tick_val/1000000, 1)
        new_tick_format = '${:}M'.format(val)
    elif tick_val >= 1000:
        val = round(tick_val/1000, 1)
        new_tick_format = '${:}K'.format(val)
    elif tick_val < 1000:
        new_tick_format = round(tick_val, 1)
    else:
        new_tick_format = tick_val

    # make new_tick_format into a string value
    new_tick_format = str(new_tick_format)
    
    # code below will keep 4.5M as is but change values such as 4.0M to 4M since that zero after the decimal isn't needed
    index_of_decimal = new_tick_format.find(".")
    
    if index_of_decimal != -1:
        value_after_decimal = new_tick_format[index_of_decimal+1]
        if value_after_decimal == "0":
            # remove the 0 after the decimal point since it's not needed
            new_tick_format = new_tick_format[0:index_of_decimal] + new_tick_format[index_of_decimal+2:]
            
    return new_tick_format
```


```python
#creating a dictionary using a for loop to
#this way I can look at all of the files at once
#rather than load them individually


DATA = {}
for file in files_list:
    key = file.split('/')[-1]
    print(file)
    try:
        df = pd.read_csv(file)
    except:
        #had one files we needed to create an except for
        #reviews was tabs seperated rather than comma seperated
        df = pd.read_csv(file, sep='\t',encoding = 'Latin-1')
    DATA[key] = df
```

    zippedData/imdb.title.crew.csv.gz
    zippedData/tmdb.movies.csv.gz
    zippedData/imdb.title.akas.csv.gz
    zippedData/imdb.title.ratings.csv.gz
    zippedData/imdb.name.basics.csv.gz
    zippedData/rt.reviews.tsv.gz
    zippedData/imdb.title.basics.csv.gz
    zippedData/rt.movie_info.tsv.gz
    zippedData/tn.movie_budgets.csv.gz
    zippedData/bom.movie_gross.csv.gz
    zippedData/imdb.title.principals.csv.gz



```python
# showing all data frames
for filename, df in DATA.items():
    print(filename)
    print(len(df))
    display(df.head())
    print()
```

    imdb.title.crew.csv.gz
    146144



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
      <th>tconst</th>
      <th>directors</th>
      <th>writers</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>tt0285252</td>
      <td>nm0899854</td>
      <td>nm0899854</td>
    </tr>
    <tr>
      <td>1</td>
      <td>tt0438973</td>
      <td>NaN</td>
      <td>nm0175726,nm1802864</td>
    </tr>
    <tr>
      <td>2</td>
      <td>tt0462036</td>
      <td>nm1940585</td>
      <td>nm1940585</td>
    </tr>
    <tr>
      <td>3</td>
      <td>tt0835418</td>
      <td>nm0151540</td>
      <td>nm0310087,nm0841532</td>
    </tr>
    <tr>
      <td>4</td>
      <td>tt0878654</td>
      <td>nm0089502,nm2291498,nm2292011</td>
      <td>nm0284943</td>
    </tr>
  </tbody>
</table>
</div>


    
    tmdb.movies.csv.gz
    26517



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
      <th>Unnamed: 0</th>
      <th>genre_ids</th>
      <th>id</th>
      <th>original_language</th>
      <th>original_title</th>
      <th>popularity</th>
      <th>release_date</th>
      <th>title</th>
      <th>vote_average</th>
      <th>vote_count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>0</td>
      <td>[12, 14, 10751]</td>
      <td>12444</td>
      <td>en</td>
      <td>Harry Potter and the Deathly Hallows: Part 1</td>
      <td>33.533</td>
      <td>2010-11-19</td>
      <td>Harry Potter and the Deathly Hallows: Part 1</td>
      <td>7.7</td>
      <td>10788</td>
    </tr>
    <tr>
      <td>1</td>
      <td>1</td>
      <td>[14, 12, 16, 10751]</td>
      <td>10191</td>
      <td>en</td>
      <td>How to Train Your Dragon</td>
      <td>28.734</td>
      <td>2010-03-26</td>
      <td>How to Train Your Dragon</td>
      <td>7.7</td>
      <td>7610</td>
    </tr>
    <tr>
      <td>2</td>
      <td>2</td>
      <td>[12, 28, 878]</td>
      <td>10138</td>
      <td>en</td>
      <td>Iron Man 2</td>
      <td>28.515</td>
      <td>2010-05-07</td>
      <td>Iron Man 2</td>
      <td>6.8</td>
      <td>12368</td>
    </tr>
    <tr>
      <td>3</td>
      <td>3</td>
      <td>[16, 35, 10751]</td>
      <td>862</td>
      <td>en</td>
      <td>Toy Story</td>
      <td>28.005</td>
      <td>1995-11-22</td>
      <td>Toy Story</td>
      <td>7.9</td>
      <td>10174</td>
    </tr>
    <tr>
      <td>4</td>
      <td>4</td>
      <td>[28, 878, 12]</td>
      <td>27205</td>
      <td>en</td>
      <td>Inception</td>
      <td>27.920</td>
      <td>2010-07-16</td>
      <td>Inception</td>
      <td>8.3</td>
      <td>22186</td>
    </tr>
  </tbody>
</table>
</div>


    
    imdb.title.akas.csv.gz
    331703



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
      <th>title_id</th>
      <th>ordering</th>
      <th>title</th>
      <th>region</th>
      <th>language</th>
      <th>types</th>
      <th>attributes</th>
      <th>is_original_title</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>tt0369610</td>
      <td>10</td>
      <td>Джурасик свят</td>
      <td>BG</td>
      <td>bg</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
    </tr>
    <tr>
      <td>1</td>
      <td>tt0369610</td>
      <td>11</td>
      <td>Jurashikku warudo</td>
      <td>JP</td>
      <td>NaN</td>
      <td>imdbDisplay</td>
      <td>NaN</td>
      <td>0.0</td>
    </tr>
    <tr>
      <td>2</td>
      <td>tt0369610</td>
      <td>12</td>
      <td>Jurassic World: O Mundo dos Dinossauros</td>
      <td>BR</td>
      <td>NaN</td>
      <td>imdbDisplay</td>
      <td>NaN</td>
      <td>0.0</td>
    </tr>
    <tr>
      <td>3</td>
      <td>tt0369610</td>
      <td>13</td>
      <td>O Mundo dos Dinossauros</td>
      <td>BR</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>short title</td>
      <td>0.0</td>
    </tr>
    <tr>
      <td>4</td>
      <td>tt0369610</td>
      <td>14</td>
      <td>Jurassic World</td>
      <td>FR</td>
      <td>NaN</td>
      <td>imdbDisplay</td>
      <td>NaN</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
</div>


    
    imdb.title.ratings.csv.gz
    73856



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
      <th>tconst</th>
      <th>averagerating</th>
      <th>numvotes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>tt10356526</td>
      <td>8.3</td>
      <td>31</td>
    </tr>
    <tr>
      <td>1</td>
      <td>tt10384606</td>
      <td>8.9</td>
      <td>559</td>
    </tr>
    <tr>
      <td>2</td>
      <td>tt1042974</td>
      <td>6.4</td>
      <td>20</td>
    </tr>
    <tr>
      <td>3</td>
      <td>tt1043726</td>
      <td>4.2</td>
      <td>50352</td>
    </tr>
    <tr>
      <td>4</td>
      <td>tt1060240</td>
      <td>6.5</td>
      <td>21</td>
    </tr>
  </tbody>
</table>
</div>


    
    imdb.name.basics.csv.gz
    606648



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
      <th>nconst</th>
      <th>primary_name</th>
      <th>birth_year</th>
      <th>death_year</th>
      <th>primary_profession</th>
      <th>known_for_titles</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>nm0061671</td>
      <td>Mary Ellen Bauder</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>miscellaneous,production_manager,producer</td>
      <td>tt0837562,tt2398241,tt0844471,tt0118553</td>
    </tr>
    <tr>
      <td>1</td>
      <td>nm0061865</td>
      <td>Joseph Bauer</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>composer,music_department,sound_department</td>
      <td>tt0896534,tt6791238,tt0287072,tt1682940</td>
    </tr>
    <tr>
      <td>2</td>
      <td>nm0062070</td>
      <td>Bruce Baum</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>miscellaneous,actor,writer</td>
      <td>tt1470654,tt0363631,tt0104030,tt0102898</td>
    </tr>
    <tr>
      <td>3</td>
      <td>nm0062195</td>
      <td>Axel Baumann</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>camera_department,cinematographer,art_department</td>
      <td>tt0114371,tt2004304,tt1618448,tt1224387</td>
    </tr>
    <tr>
      <td>4</td>
      <td>nm0062798</td>
      <td>Pete Baxter</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>production_designer,art_department,set_decorator</td>
      <td>tt0452644,tt0452692,tt3458030,tt2178256</td>
    </tr>
  </tbody>
</table>
</div>


    
    rt.reviews.tsv.gz
    54432



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
      <th>id</th>
      <th>review</th>
      <th>rating</th>
      <th>fresh</th>
      <th>critic</th>
      <th>top_critic</th>
      <th>publisher</th>
      <th>date</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>3</td>
      <td>A distinctly gallows take on contemporary fina...</td>
      <td>3/5</td>
      <td>fresh</td>
      <td>PJ Nabarro</td>
      <td>0</td>
      <td>Patrick Nabarro</td>
      <td>November 10, 2018</td>
    </tr>
    <tr>
      <td>1</td>
      <td>3</td>
      <td>It's an allegory in search of a meaning that n...</td>
      <td>NaN</td>
      <td>rotten</td>
      <td>Annalee Newitz</td>
      <td>0</td>
      <td>io9.com</td>
      <td>May 23, 2018</td>
    </tr>
    <tr>
      <td>2</td>
      <td>3</td>
      <td>... life lived in a bubble in financial dealin...</td>
      <td>NaN</td>
      <td>fresh</td>
      <td>Sean Axmaker</td>
      <td>0</td>
      <td>Stream on Demand</td>
      <td>January 4, 2018</td>
    </tr>
    <tr>
      <td>3</td>
      <td>3</td>
      <td>Continuing along a line introduced in last yea...</td>
      <td>NaN</td>
      <td>fresh</td>
      <td>Daniel Kasman</td>
      <td>0</td>
      <td>MUBI</td>
      <td>November 16, 2017</td>
    </tr>
    <tr>
      <td>4</td>
      <td>3</td>
      <td>... a perverse twist on neorealism...</td>
      <td>NaN</td>
      <td>fresh</td>
      <td>NaN</td>
      <td>0</td>
      <td>Cinema Scope</td>
      <td>October 12, 2017</td>
    </tr>
  </tbody>
</table>
</div>


    
    imdb.title.basics.csv.gz
    146144



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
      <th>tconst</th>
      <th>primary_title</th>
      <th>original_title</th>
      <th>start_year</th>
      <th>runtime_minutes</th>
      <th>genres</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>tt0063540</td>
      <td>Sunghursh</td>
      <td>Sunghursh</td>
      <td>2013</td>
      <td>175.0</td>
      <td>Action,Crime,Drama</td>
    </tr>
    <tr>
      <td>1</td>
      <td>tt0066787</td>
      <td>One Day Before the Rainy Season</td>
      <td>Ashad Ka Ek Din</td>
      <td>2019</td>
      <td>114.0</td>
      <td>Biography,Drama</td>
    </tr>
    <tr>
      <td>2</td>
      <td>tt0069049</td>
      <td>The Other Side of the Wind</td>
      <td>The Other Side of the Wind</td>
      <td>2018</td>
      <td>122.0</td>
      <td>Drama</td>
    </tr>
    <tr>
      <td>3</td>
      <td>tt0069204</td>
      <td>Sabse Bada Sukh</td>
      <td>Sabse Bada Sukh</td>
      <td>2018</td>
      <td>NaN</td>
      <td>Comedy,Drama</td>
    </tr>
    <tr>
      <td>4</td>
      <td>tt0100275</td>
      <td>The Wandering Soap Opera</td>
      <td>La Telenovela Errante</td>
      <td>2017</td>
      <td>80.0</td>
      <td>Comedy,Drama,Fantasy</td>
    </tr>
  </tbody>
</table>
</div>


    
    rt.movie_info.tsv.gz
    1560



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
      <th>id</th>
      <th>synopsis</th>
      <th>rating</th>
      <th>genre</th>
      <th>director</th>
      <th>writer</th>
      <th>theater_date</th>
      <th>dvd_date</th>
      <th>currency</th>
      <th>box_office</th>
      <th>runtime</th>
      <th>studio</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>1</td>
      <td>This gritty, fast-paced, and innovative police...</td>
      <td>R</td>
      <td>Action and Adventure|Classics|Drama</td>
      <td>William Friedkin</td>
      <td>Ernest Tidyman</td>
      <td>Oct 9, 1971</td>
      <td>Sep 25, 2001</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>104 minutes</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>1</td>
      <td>3</td>
      <td>New York City, not-too-distant-future: Eric Pa...</td>
      <td>R</td>
      <td>Drama|Science Fiction and Fantasy</td>
      <td>David Cronenberg</td>
      <td>David Cronenberg|Don DeLillo</td>
      <td>Aug 17, 2012</td>
      <td>Jan 1, 2013</td>
      <td>$</td>
      <td>600,000</td>
      <td>108 minutes</td>
      <td>Entertainment One</td>
    </tr>
    <tr>
      <td>2</td>
      <td>5</td>
      <td>Illeana Douglas delivers a superb performance ...</td>
      <td>R</td>
      <td>Drama|Musical and Performing Arts</td>
      <td>Allison Anders</td>
      <td>Allison Anders</td>
      <td>Sep 13, 1996</td>
      <td>Apr 18, 2000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>116 minutes</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>3</td>
      <td>6</td>
      <td>Michael Douglas runs afoul of a treacherous su...</td>
      <td>R</td>
      <td>Drama|Mystery and Suspense</td>
      <td>Barry Levinson</td>
      <td>Paul Attanasio|Michael Crichton</td>
      <td>Dec 9, 1994</td>
      <td>Aug 27, 1997</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>128 minutes</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>4</td>
      <td>7</td>
      <td>NaN</td>
      <td>NR</td>
      <td>Drama|Romance</td>
      <td>Rodney Bennett</td>
      <td>Giles Cooper</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>200 minutes</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>


    
    tn.movie_budgets.csv.gz
    5782



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
      <th>id</th>
      <th>release_date</th>
      <th>movie</th>
      <th>production_budget</th>
      <th>domestic_gross</th>
      <th>worldwide_gross</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>1</td>
      <td>Dec 18, 2009</td>
      <td>Avatar</td>
      <td>$425,000,000</td>
      <td>$760,507,625</td>
      <td>$2,776,345,279</td>
    </tr>
    <tr>
      <td>1</td>
      <td>2</td>
      <td>May 20, 2011</td>
      <td>Pirates of the Caribbean: On Stranger Tides</td>
      <td>$410,600,000</td>
      <td>$241,063,875</td>
      <td>$1,045,663,875</td>
    </tr>
    <tr>
      <td>2</td>
      <td>3</td>
      <td>Jun 7, 2019</td>
      <td>Dark Phoenix</td>
      <td>$350,000,000</td>
      <td>$42,762,350</td>
      <td>$149,762,350</td>
    </tr>
    <tr>
      <td>3</td>
      <td>4</td>
      <td>May 1, 2015</td>
      <td>Avengers: Age of Ultron</td>
      <td>$330,600,000</td>
      <td>$459,005,868</td>
      <td>$1,403,013,963</td>
    </tr>
    <tr>
      <td>4</td>
      <td>5</td>
      <td>Dec 15, 2017</td>
      <td>Star Wars Ep. VIII: The Last Jedi</td>
      <td>$317,000,000</td>
      <td>$620,181,382</td>
      <td>$1,316,721,747</td>
    </tr>
  </tbody>
</table>
</div>


    
    bom.movie_gross.csv.gz
    3387



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
      <th>title</th>
      <th>studio</th>
      <th>domestic_gross</th>
      <th>foreign_gross</th>
      <th>year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>Toy Story 3</td>
      <td>BV</td>
      <td>415000000.0</td>
      <td>652000000</td>
      <td>2010</td>
    </tr>
    <tr>
      <td>1</td>
      <td>Alice in Wonderland (2010)</td>
      <td>BV</td>
      <td>334200000.0</td>
      <td>691300000</td>
      <td>2010</td>
    </tr>
    <tr>
      <td>2</td>
      <td>Harry Potter and the Deathly Hallows Part 1</td>
      <td>WB</td>
      <td>296000000.0</td>
      <td>664300000</td>
      <td>2010</td>
    </tr>
    <tr>
      <td>3</td>
      <td>Inception</td>
      <td>WB</td>
      <td>292600000.0</td>
      <td>535700000</td>
      <td>2010</td>
    </tr>
    <tr>
      <td>4</td>
      <td>Shrek Forever After</td>
      <td>P/DW</td>
      <td>238700000.0</td>
      <td>513900000</td>
      <td>2010</td>
    </tr>
  </tbody>
</table>
</div>


    
    imdb.title.principals.csv.gz
    1028186



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
      <th>tconst</th>
      <th>ordering</th>
      <th>nconst</th>
      <th>category</th>
      <th>job</th>
      <th>characters</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>tt0111414</td>
      <td>1</td>
      <td>nm0246005</td>
      <td>actor</td>
      <td>NaN</td>
      <td>["The Man"]</td>
    </tr>
    <tr>
      <td>1</td>
      <td>tt0111414</td>
      <td>2</td>
      <td>nm0398271</td>
      <td>director</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>2</td>
      <td>tt0111414</td>
      <td>3</td>
      <td>nm3739909</td>
      <td>producer</td>
      <td>producer</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>3</td>
      <td>tt0323808</td>
      <td>10</td>
      <td>nm0059247</td>
      <td>editor</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>4</td>
      <td>tt0323808</td>
      <td>1</td>
      <td>nm3579312</td>
      <td>actress</td>
      <td>NaN</td>
      <td>["Beth Boothby"]</td>
    </tr>
  </tbody>
</table>
</div>


    


## Genre - Done


```python
df_tn_budget = pd.read_csv(files_list[8])
df_tn_budget.head(3)
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
      <th>id</th>
      <th>release_date</th>
      <th>movie</th>
      <th>production_budget</th>
      <th>domestic_gross</th>
      <th>worldwide_gross</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>1</td>
      <td>Dec 18, 2009</td>
      <td>Avatar</td>
      <td>$425,000,000</td>
      <td>$760,507,625</td>
      <td>$2,776,345,279</td>
    </tr>
    <tr>
      <td>1</td>
      <td>2</td>
      <td>May 20, 2011</td>
      <td>Pirates of the Caribbean: On Stranger Tides</td>
      <td>$410,600,000</td>
      <td>$241,063,875</td>
      <td>$1,045,663,875</td>
    </tr>
    <tr>
      <td>2</td>
      <td>3</td>
      <td>Jun 7, 2019</td>
      <td>Dark Phoenix</td>
      <td>$350,000,000</td>
      <td>$42,762,350</td>
      <td>$149,762,350</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_imdb_genres = pd.read_csv(files_list[6])
df_imdb_genres.head(3)
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
      <th>tconst</th>
      <th>primary_title</th>
      <th>original_title</th>
      <th>start_year</th>
      <th>runtime_minutes</th>
      <th>genres</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>tt0063540</td>
      <td>Sunghursh</td>
      <td>Sunghursh</td>
      <td>2013</td>
      <td>175.0</td>
      <td>Action,Crime,Drama</td>
    </tr>
    <tr>
      <td>1</td>
      <td>tt0066787</td>
      <td>One Day Before the Rainy Season</td>
      <td>Ashad Ka Ek Din</td>
      <td>2019</td>
      <td>114.0</td>
      <td>Biography,Drama</td>
    </tr>
    <tr>
      <td>2</td>
      <td>tt0069049</td>
      <td>The Other Side of the Wind</td>
      <td>The Other Side of the Wind</td>
      <td>2018</td>
      <td>122.0</td>
      <td>Drama</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Merging two dataframes to compare genres and worldwide_gross
df_merge = pd.merge(df_tn_budget, df_imdb_genres, left_on = 'movie', right_on = 'primary_title')
df_merge
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
      <th>id</th>
      <th>release_date</th>
      <th>movie</th>
      <th>production_budget</th>
      <th>domestic_gross</th>
      <th>worldwide_gross</th>
      <th>tconst</th>
      <th>primary_title</th>
      <th>original_title</th>
      <th>start_year</th>
      <th>runtime_minutes</th>
      <th>genres</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>1</td>
      <td>Dec 18, 2009</td>
      <td>Avatar</td>
      <td>$425,000,000</td>
      <td>$760,507,625</td>
      <td>$2,776,345,279</td>
      <td>tt1775309</td>
      <td>Avatar</td>
      <td>Abatâ</td>
      <td>2011</td>
      <td>93.0</td>
      <td>Horror</td>
    </tr>
    <tr>
      <td>1</td>
      <td>2</td>
      <td>May 20, 2011</td>
      <td>Pirates of the Caribbean: On Stranger Tides</td>
      <td>$410,600,000</td>
      <td>$241,063,875</td>
      <td>$1,045,663,875</td>
      <td>tt1298650</td>
      <td>Pirates of the Caribbean: On Stranger Tides</td>
      <td>Pirates of the Caribbean: On Stranger Tides</td>
      <td>2011</td>
      <td>136.0</td>
      <td>Action,Adventure,Fantasy</td>
    </tr>
    <tr>
      <td>2</td>
      <td>3</td>
      <td>Jun 7, 2019</td>
      <td>Dark Phoenix</td>
      <td>$350,000,000</td>
      <td>$42,762,350</td>
      <td>$149,762,350</td>
      <td>tt6565702</td>
      <td>Dark Phoenix</td>
      <td>Dark Phoenix</td>
      <td>2019</td>
      <td>113.0</td>
      <td>Action,Adventure,Sci-Fi</td>
    </tr>
    <tr>
      <td>3</td>
      <td>4</td>
      <td>May 1, 2015</td>
      <td>Avengers: Age of Ultron</td>
      <td>$330,600,000</td>
      <td>$459,005,868</td>
      <td>$1,403,013,963</td>
      <td>tt2395427</td>
      <td>Avengers: Age of Ultron</td>
      <td>Avengers: Age of Ultron</td>
      <td>2015</td>
      <td>141.0</td>
      <td>Action,Adventure,Sci-Fi</td>
    </tr>
    <tr>
      <td>4</td>
      <td>7</td>
      <td>Apr 27, 2018</td>
      <td>Avengers: Infinity War</td>
      <td>$300,000,000</td>
      <td>$678,815,482</td>
      <td>$2,048,134,200</td>
      <td>tt4154756</td>
      <td>Avengers: Infinity War</td>
      <td>Avengers: Infinity War</td>
      <td>2018</td>
      <td>149.0</td>
      <td>Action,Adventure,Sci-Fi</td>
    </tr>
    <tr>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <td>3810</td>
      <td>68</td>
      <td>Jul 6, 2001</td>
      <td>Cure</td>
      <td>$10,000</td>
      <td>$94,596</td>
      <td>$94,596</td>
      <td>tt5936960</td>
      <td>Cure</td>
      <td>Cure</td>
      <td>2014</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>3811</td>
      <td>70</td>
      <td>Apr 1, 1996</td>
      <td>Bang</td>
      <td>$10,000</td>
      <td>$527</td>
      <td>$527</td>
      <td>tt6616538</td>
      <td>Bang</td>
      <td>Bang</td>
      <td>2015</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>3812</td>
      <td>73</td>
      <td>Jan 13, 2012</td>
      <td>Newlyweds</td>
      <td>$9,000</td>
      <td>$4,584</td>
      <td>$4,584</td>
      <td>tt1880418</td>
      <td>Newlyweds</td>
      <td>Newlyweds</td>
      <td>2011</td>
      <td>95.0</td>
      <td>Comedy,Drama</td>
    </tr>
    <tr>
      <td>3813</td>
      <td>78</td>
      <td>Dec 31, 2018</td>
      <td>Red 11</td>
      <td>$7,000</td>
      <td>$0</td>
      <td>$0</td>
      <td>tt7837402</td>
      <td>Red 11</td>
      <td>Red 11</td>
      <td>2019</td>
      <td>77.0</td>
      <td>Horror,Sci-Fi,Thriller</td>
    </tr>
    <tr>
      <td>3814</td>
      <td>81</td>
      <td>Sep 29, 2015</td>
      <td>A Plague So Pleasant</td>
      <td>$1,400</td>
      <td>$0</td>
      <td>$0</td>
      <td>tt2107644</td>
      <td>A Plague So Pleasant</td>
      <td>A Plague So Pleasant</td>
      <td>2013</td>
      <td>76.0</td>
      <td>Drama,Horror,Thriller</td>
    </tr>
  </tbody>
</table>
<p>3815 rows × 12 columns</p>
</div>




```python
# Viewing which columns have null values in df_merge
df_merge.isna().sum()
```




    id                     0
    release_date           0
    movie                  0
    production_budget      0
    domestic_gross         0
    worldwide_gross        0
    tconst                 0
    primary_title          0
    original_title         1
    start_year             0
    runtime_minutes      487
    genres                72
    dtype: int64




```python
# Testing how to convert string to integers, while removing symbols
test = df_merge['domestic_gross'][0]
test
```




    '$760,507,625'




```python
type(test)
```




    str




```python
test.replace(',','').replace('$','')
```




    '760507625'




```python
#converted production, domestic and worldwide into integers
df_merge['domestic_gross'] = df_merge['domestic_gross'].map(lambda x: float(x.replace(',','').replace('$','')))
```


```python
df_merge['production_budget'] = df_merge['production_budget'].map(lambda x: float(x.replace(',','').replace('$','')))
```


```python
df_merge['worldwide_gross'] = df_merge['worldwide_gross'].map(lambda x: float(x.replace(',','').replace('$','')))
```


```python
df_merge
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
      <th>id</th>
      <th>release_date</th>
      <th>movie</th>
      <th>production_budget</th>
      <th>domestic_gross</th>
      <th>worldwide_gross</th>
      <th>tconst</th>
      <th>primary_title</th>
      <th>original_title</th>
      <th>start_year</th>
      <th>runtime_minutes</th>
      <th>genres</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>1</td>
      <td>Dec 18, 2009</td>
      <td>Avatar</td>
      <td>425000000.0</td>
      <td>760507625.0</td>
      <td>2.776345e+09</td>
      <td>tt1775309</td>
      <td>Avatar</td>
      <td>Abatâ</td>
      <td>2011</td>
      <td>93.0</td>
      <td>Horror</td>
    </tr>
    <tr>
      <td>1</td>
      <td>2</td>
      <td>May 20, 2011</td>
      <td>Pirates of the Caribbean: On Stranger Tides</td>
      <td>410600000.0</td>
      <td>241063875.0</td>
      <td>1.045664e+09</td>
      <td>tt1298650</td>
      <td>Pirates of the Caribbean: On Stranger Tides</td>
      <td>Pirates of the Caribbean: On Stranger Tides</td>
      <td>2011</td>
      <td>136.0</td>
      <td>Action,Adventure,Fantasy</td>
    </tr>
    <tr>
      <td>2</td>
      <td>3</td>
      <td>Jun 7, 2019</td>
      <td>Dark Phoenix</td>
      <td>350000000.0</td>
      <td>42762350.0</td>
      <td>1.497624e+08</td>
      <td>tt6565702</td>
      <td>Dark Phoenix</td>
      <td>Dark Phoenix</td>
      <td>2019</td>
      <td>113.0</td>
      <td>Action,Adventure,Sci-Fi</td>
    </tr>
    <tr>
      <td>3</td>
      <td>4</td>
      <td>May 1, 2015</td>
      <td>Avengers: Age of Ultron</td>
      <td>330600000.0</td>
      <td>459005868.0</td>
      <td>1.403014e+09</td>
      <td>tt2395427</td>
      <td>Avengers: Age of Ultron</td>
      <td>Avengers: Age of Ultron</td>
      <td>2015</td>
      <td>141.0</td>
      <td>Action,Adventure,Sci-Fi</td>
    </tr>
    <tr>
      <td>4</td>
      <td>7</td>
      <td>Apr 27, 2018</td>
      <td>Avengers: Infinity War</td>
      <td>300000000.0</td>
      <td>678815482.0</td>
      <td>2.048134e+09</td>
      <td>tt4154756</td>
      <td>Avengers: Infinity War</td>
      <td>Avengers: Infinity War</td>
      <td>2018</td>
      <td>149.0</td>
      <td>Action,Adventure,Sci-Fi</td>
    </tr>
    <tr>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <td>3810</td>
      <td>68</td>
      <td>Jul 6, 2001</td>
      <td>Cure</td>
      <td>10000.0</td>
      <td>94596.0</td>
      <td>9.459600e+04</td>
      <td>tt5936960</td>
      <td>Cure</td>
      <td>Cure</td>
      <td>2014</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>3811</td>
      <td>70</td>
      <td>Apr 1, 1996</td>
      <td>Bang</td>
      <td>10000.0</td>
      <td>527.0</td>
      <td>5.270000e+02</td>
      <td>tt6616538</td>
      <td>Bang</td>
      <td>Bang</td>
      <td>2015</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>3812</td>
      <td>73</td>
      <td>Jan 13, 2012</td>
      <td>Newlyweds</td>
      <td>9000.0</td>
      <td>4584.0</td>
      <td>4.584000e+03</td>
      <td>tt1880418</td>
      <td>Newlyweds</td>
      <td>Newlyweds</td>
      <td>2011</td>
      <td>95.0</td>
      <td>Comedy,Drama</td>
    </tr>
    <tr>
      <td>3813</td>
      <td>78</td>
      <td>Dec 31, 2018</td>
      <td>Red 11</td>
      <td>7000.0</td>
      <td>0.0</td>
      <td>0.000000e+00</td>
      <td>tt7837402</td>
      <td>Red 11</td>
      <td>Red 11</td>
      <td>2019</td>
      <td>77.0</td>
      <td>Horror,Sci-Fi,Thriller</td>
    </tr>
    <tr>
      <td>3814</td>
      <td>81</td>
      <td>Sep 29, 2015</td>
      <td>A Plague So Pleasant</td>
      <td>1400.0</td>
      <td>0.0</td>
      <td>0.000000e+00</td>
      <td>tt2107644</td>
      <td>A Plague So Pleasant</td>
      <td>A Plague So Pleasant</td>
      <td>2013</td>
      <td>76.0</td>
      <td>Drama,Horror,Thriller</td>
    </tr>
  </tbody>
</table>
<p>3815 rows × 12 columns</p>
</div>




```python
#removed columns with null values in genre
df_merge = df_merge[df_merge['genres'].notna()]
df_merge.isna().sum()
```




    id                     0
    release_date           0
    movie                  0
    production_budget      0
    domestic_gross         0
    worldwide_gross        0
    tconst                 0
    primary_title          0
    original_title         0
    start_year             0
    runtime_minutes      434
    genres                 0
    dtype: int64




```python
df_merge['Profits'] = (df_merge['worldwide_gross'] - df_merge['production_budget'])
df_merge.head()
```

    /opt/anaconda3/envs/learn-env/lib/python3.6/site-packages/ipykernel_launcher.py:1: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      """Entry point for launching an IPython kernel.





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
      <th>id</th>
      <th>release_date</th>
      <th>movie</th>
      <th>production_budget</th>
      <th>domestic_gross</th>
      <th>worldwide_gross</th>
      <th>tconst</th>
      <th>primary_title</th>
      <th>original_title</th>
      <th>start_year</th>
      <th>runtime_minutes</th>
      <th>genres</th>
      <th>Profits</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>1</td>
      <td>Dec 18, 2009</td>
      <td>Avatar</td>
      <td>425000000.0</td>
      <td>760507625.0</td>
      <td>2.776345e+09</td>
      <td>tt1775309</td>
      <td>Avatar</td>
      <td>Abatâ</td>
      <td>2011</td>
      <td>93.0</td>
      <td>Horror</td>
      <td>2.351345e+09</td>
    </tr>
    <tr>
      <td>1</td>
      <td>2</td>
      <td>May 20, 2011</td>
      <td>Pirates of the Caribbean: On Stranger Tides</td>
      <td>410600000.0</td>
      <td>241063875.0</td>
      <td>1.045664e+09</td>
      <td>tt1298650</td>
      <td>Pirates of the Caribbean: On Stranger Tides</td>
      <td>Pirates of the Caribbean: On Stranger Tides</td>
      <td>2011</td>
      <td>136.0</td>
      <td>Action,Adventure,Fantasy</td>
      <td>6.350639e+08</td>
    </tr>
    <tr>
      <td>2</td>
      <td>3</td>
      <td>Jun 7, 2019</td>
      <td>Dark Phoenix</td>
      <td>350000000.0</td>
      <td>42762350.0</td>
      <td>1.497624e+08</td>
      <td>tt6565702</td>
      <td>Dark Phoenix</td>
      <td>Dark Phoenix</td>
      <td>2019</td>
      <td>113.0</td>
      <td>Action,Adventure,Sci-Fi</td>
      <td>-2.002376e+08</td>
    </tr>
    <tr>
      <td>3</td>
      <td>4</td>
      <td>May 1, 2015</td>
      <td>Avengers: Age of Ultron</td>
      <td>330600000.0</td>
      <td>459005868.0</td>
      <td>1.403014e+09</td>
      <td>tt2395427</td>
      <td>Avengers: Age of Ultron</td>
      <td>Avengers: Age of Ultron</td>
      <td>2015</td>
      <td>141.0</td>
      <td>Action,Adventure,Sci-Fi</td>
      <td>1.072414e+09</td>
    </tr>
    <tr>
      <td>4</td>
      <td>7</td>
      <td>Apr 27, 2018</td>
      <td>Avengers: Infinity War</td>
      <td>300000000.0</td>
      <td>678815482.0</td>
      <td>2.048134e+09</td>
      <td>tt4154756</td>
      <td>Avengers: Infinity War</td>
      <td>Avengers: Infinity War</td>
      <td>2018</td>
      <td>149.0</td>
      <td>Action,Adventure,Sci-Fi</td>
      <td>1.748134e+09</td>
    </tr>
  </tbody>
</table>
</div>




```python
# df_merge['genres'] = df_merge['genres'].str.split(",")
```


```python
# Creates a long string 
combined = ','.join(df_merge['genres'])
# splitting on ',' to make a list and using set to find the unique values
all_genres = list(set(combined.split(',')))
#achieved finding all Genres used
all_genres
```




    ['Horror',
     'War',
     'Action',
     'Sport',
     'Thriller',
     'Family',
     'Fantasy',
     'Comedy',
     'Reality-TV',
     'Music',
     'Sci-Fi',
     'Biography',
     'Romance',
     'Musical',
     'Animation',
     'Adventure',
     'Western',
     'Documentary',
     'News',
     'History',
     'Crime',
     'Drama',
     'Mystery']




```python
# create empy dataframe
genre_df = pd.DataFrame()
for genre in all_genres:
    genre_df[genre] = df_merge['genres'].str.contains(genre).astype(int)
genre_df
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
      <th>Horror</th>
      <th>War</th>
      <th>Action</th>
      <th>Sport</th>
      <th>Thriller</th>
      <th>Family</th>
      <th>Fantasy</th>
      <th>Comedy</th>
      <th>Reality-TV</th>
      <th>Music</th>
      <th>...</th>
      <th>Musical</th>
      <th>Animation</th>
      <th>Adventure</th>
      <th>Western</th>
      <th>Documentary</th>
      <th>News</th>
      <th>History</th>
      <th>Crime</th>
      <th>Drama</th>
      <th>Mystery</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <td>3</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <td>4</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <td>3808</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <td>3809</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <td>3812</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <td>3813</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <td>3814</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>3743 rows × 23 columns</p>
</div>




```python
#tacking on the above df to my merge df
df = pd.concat([df_merge,genre_df], axis = 1)
df
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
      <th>id</th>
      <th>release_date</th>
      <th>movie</th>
      <th>production_budget</th>
      <th>domestic_gross</th>
      <th>worldwide_gross</th>
      <th>tconst</th>
      <th>primary_title</th>
      <th>original_title</th>
      <th>start_year</th>
      <th>...</th>
      <th>Musical</th>
      <th>Animation</th>
      <th>Adventure</th>
      <th>Western</th>
      <th>Documentary</th>
      <th>News</th>
      <th>History</th>
      <th>Crime</th>
      <th>Drama</th>
      <th>Mystery</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>1</td>
      <td>Dec 18, 2009</td>
      <td>Avatar</td>
      <td>425000000.0</td>
      <td>760507625.0</td>
      <td>2.776345e+09</td>
      <td>tt1775309</td>
      <td>Avatar</td>
      <td>Abatâ</td>
      <td>2011</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <td>1</td>
      <td>2</td>
      <td>May 20, 2011</td>
      <td>Pirates of the Caribbean: On Stranger Tides</td>
      <td>410600000.0</td>
      <td>241063875.0</td>
      <td>1.045664e+09</td>
      <td>tt1298650</td>
      <td>Pirates of the Caribbean: On Stranger Tides</td>
      <td>Pirates of the Caribbean: On Stranger Tides</td>
      <td>2011</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <td>2</td>
      <td>3</td>
      <td>Jun 7, 2019</td>
      <td>Dark Phoenix</td>
      <td>350000000.0</td>
      <td>42762350.0</td>
      <td>1.497624e+08</td>
      <td>tt6565702</td>
      <td>Dark Phoenix</td>
      <td>Dark Phoenix</td>
      <td>2019</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <td>3</td>
      <td>4</td>
      <td>May 1, 2015</td>
      <td>Avengers: Age of Ultron</td>
      <td>330600000.0</td>
      <td>459005868.0</td>
      <td>1.403014e+09</td>
      <td>tt2395427</td>
      <td>Avengers: Age of Ultron</td>
      <td>Avengers: Age of Ultron</td>
      <td>2015</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <td>4</td>
      <td>7</td>
      <td>Apr 27, 2018</td>
      <td>Avengers: Infinity War</td>
      <td>300000000.0</td>
      <td>678815482.0</td>
      <td>2.048134e+09</td>
      <td>tt4154756</td>
      <td>Avengers: Infinity War</td>
      <td>Avengers: Infinity War</td>
      <td>2018</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <td>3808</td>
      <td>67</td>
      <td>Apr 28, 2006</td>
      <td>Clean</td>
      <td>10000.0</td>
      <td>138711.0</td>
      <td>1.387110e+05</td>
      <td>tt6619196</td>
      <td>Clean</td>
      <td>Clean</td>
      <td>2017</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <td>3809</td>
      <td>68</td>
      <td>Jul 6, 2001</td>
      <td>Cure</td>
      <td>10000.0</td>
      <td>94596.0</td>
      <td>9.459600e+04</td>
      <td>tt1872026</td>
      <td>Cure</td>
      <td>Cure</td>
      <td>2011</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <td>3812</td>
      <td>73</td>
      <td>Jan 13, 2012</td>
      <td>Newlyweds</td>
      <td>9000.0</td>
      <td>4584.0</td>
      <td>4.584000e+03</td>
      <td>tt1880418</td>
      <td>Newlyweds</td>
      <td>Newlyweds</td>
      <td>2011</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <td>3813</td>
      <td>78</td>
      <td>Dec 31, 2018</td>
      <td>Red 11</td>
      <td>7000.0</td>
      <td>0.0</td>
      <td>0.000000e+00</td>
      <td>tt7837402</td>
      <td>Red 11</td>
      <td>Red 11</td>
      <td>2019</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <td>3814</td>
      <td>81</td>
      <td>Sep 29, 2015</td>
      <td>A Plague So Pleasant</td>
      <td>1400.0</td>
      <td>0.0</td>
      <td>0.000000e+00</td>
      <td>tt2107644</td>
      <td>A Plague So Pleasant</td>
      <td>A Plague So Pleasant</td>
      <td>2013</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>3743 rows × 36 columns</p>
</div>




```python
#viewing my column names to make sure everythings there
list(df.columns.values)
```




    ['id',
     'release_date',
     'movie',
     'production_budget',
     'domestic_gross',
     'worldwide_gross',
     'tconst',
     'primary_title',
     'original_title',
     'start_year',
     'runtime_minutes',
     'genres',
     'Profits',
     'Horror',
     'War',
     'Action',
     'Sport',
     'Thriller',
     'Family',
     'Fantasy',
     'Comedy',
     'Reality-TV',
     'Music',
     'Sci-Fi',
     'Biography',
     'Romance',
     'Musical',
     'Animation',
     'Adventure',
     'Western',
     'Documentary',
     'News',
     'History',
     'Crime',
     'Drama',
     'Mystery']




```python
#taking any rows that fit into the genres
genre_dfs = {}
for genre in all_genres:
    genre_dfs[genre] = df.groupby(genre).get_group(1)
genre_dfs.keys()
```




    dict_keys(['Horror', 'War', 'Action', 'Sport', 'Thriller', 'Family', 'Fantasy', 'Comedy', 'Reality-TV', 'Music', 'Sci-Fi', 'Biography', 'Romance', 'Musical', 'Animation', 'Adventure', 'Western', 'Documentary', 'News', 'History', 'Crime', 'Drama', 'Mystery'])




```python
#column I'm interested in plotting
profits = ['Profits']
#another dictionary for my column above
plot_dict = {}

for col in profits:
    #this is where I created the dictionary 
    plot_dict[col] = {}
    #for every genre, I filled in every column with the genre df's and pulling it out with the column
    for genre,genre_df in genre_dfs.items():
        plot_dict[col][genre] = genre_df[col]
plot_dict.keys()
```




    dict_keys(['Profits'])




```python
# plt.style.available
```




    ['seaborn-dark',
     'seaborn-darkgrid',
     'seaborn-ticks',
     'fivethirtyeight',
     'seaborn-whitegrid',
     'classic',
     '_classic_test',
     'fast',
     'seaborn-talk',
     'seaborn-dark-palette',
     'seaborn-bright',
     'seaborn-pastel',
     'grayscale',
     'seaborn-notebook',
     'ggplot',
     'seaborn-colorblind',
     'seaborn-muted',
     'seaborn',
     'Solarize_Light2',
     'seaborn-paper',
     'bmh',
     'tableau-colorblind10',
     'seaborn-white',
     'dark_background',
     'seaborn-poster',
     'seaborn-deep']




```python
# #created my new plot
# for style in plt.style.available:

#     with plt.style.context(style):


#         revenue = pd.DataFrame.from_dict(plot_dict['Profits'])

#         new_figure = plt.figure(figsize=(20,15))
#         ax = plt.axes()

#         sns.barplot(data=revenue,
#                     orient='h',
#                     ci=68).set_title(f'{style}',#'Most profitable Genres',
#                     fontsize = 30)

#         ax.set(xlabel = 'Profits', ylabel = 'Movie Genre')
#         plt.xticks(rotation = 45)
#         ax.xaxis.set_major_formatter(FuncFormatter(reformat_large_tick_values));
```


```python
#created my new plot
#get the mean for profits
revenue = pd.DataFrame.from_dict(plot_dict['Profits'])
#put this into descending order
genre_order = revenue.mean().sort_values(ascending = False).index
genre_order
```




    Index(['Animation', 'Adventure', 'Musical', 'Sci-Fi', 'Fantasy', 'Action',
           'Family', 'Music', 'Comedy', 'Thriller', 'Mystery', 'Sport', 'Horror',
           'Biography', 'History', 'Romance', 'Documentary', 'Crime', 'Drama',
           'War', 'Western', 'News', 'Reality-TV'],
          dtype='object')




```python
with plt.style.context('seaborn-poster'):

    new_figure = plt.figure(figsize=(20,15))
    ax = plt.axes()

    sns.barplot(data=revenue, order = genre_order,
                orient='h',
                ci=68).set_title('Most profitable Genres',
                fontsize = 30)

    ax.set(xlabel = 'Profits', ylabel = 'Movie Genre')
    plt.xticks(rotation = 45)
    ax.xaxis.set_major_formatter(FuncFormatter(reformat_large_tick_values));
```


![png](output_37_0.png)


## Budget - Done
### What's the average budget spent? What average budget had the highest ROI?


```python
#converted production, domestic and worldwide into integers
df_tn_budget['domestic_gross'] = df_tn_budget['domestic_gross'].map(lambda x: float(x.replace(',','').replace('$','')))
df_tn_budget['production_budget'] = df_tn_budget['production_budget'].map(lambda x: float(x.replace(',','').replace('$','')))
df_tn_budget['worldwide_gross'] = df_tn_budget['worldwide_gross'].map(lambda x: float(x.replace(',','').replace('$','')))
```


```python
df_tn_budget['Profits'] = (df_tn_budget['worldwide_gross'] - df_tn_budget['production_budget'])
```


```python
#Organizing from highest profits to lowest profits
df_tn_budget.sort_values(by = ['Profits'], ascending = False, inplace = True)
df_tn_budget.head(100)
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
      <th>id</th>
      <th>release_date</th>
      <th>movie</th>
      <th>production_budget</th>
      <th>domestic_gross</th>
      <th>worldwide_gross</th>
      <th>Profits</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>1</td>
      <td>Dec 18, 2009</td>
      <td>Avatar</td>
      <td>425000000.0</td>
      <td>760507625.0</td>
      <td>2.776345e+09</td>
      <td>2.351345e+09</td>
    </tr>
    <tr>
      <td>42</td>
      <td>43</td>
      <td>Dec 19, 1997</td>
      <td>Titanic</td>
      <td>200000000.0</td>
      <td>659363944.0</td>
      <td>2.208208e+09</td>
      <td>2.008208e+09</td>
    </tr>
    <tr>
      <td>6</td>
      <td>7</td>
      <td>Apr 27, 2018</td>
      <td>Avengers: Infinity War</td>
      <td>300000000.0</td>
      <td>678815482.0</td>
      <td>2.048134e+09</td>
      <td>1.748134e+09</td>
    </tr>
    <tr>
      <td>5</td>
      <td>6</td>
      <td>Dec 18, 2015</td>
      <td>Star Wars Ep. VII: The Force Awakens</td>
      <td>306000000.0</td>
      <td>936662225.0</td>
      <td>2.053311e+09</td>
      <td>1.747311e+09</td>
    </tr>
    <tr>
      <td>33</td>
      <td>34</td>
      <td>Jun 12, 2015</td>
      <td>Jurassic World</td>
      <td>215000000.0</td>
      <td>652270625.0</td>
      <td>1.648855e+09</td>
      <td>1.433855e+09</td>
    </tr>
    <tr>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <td>2159</td>
      <td>60</td>
      <td>Feb 25, 2004</td>
      <td>The Passion of the Christ</td>
      <td>25000000.0</td>
      <td>370782930.0</td>
      <td>6.223419e+08</td>
      <td>5.973419e+08</td>
    </tr>
    <tr>
      <td>49</td>
      <td>50</td>
      <td>Jun 30, 2004</td>
      <td>Spider-Man 2</td>
      <td>200000000.0</td>
      <td>373524485.0</td>
      <td>7.951107e+08</td>
      <td>5.951107e+08</td>
    </tr>
    <tr>
      <td>126</td>
      <td>27</td>
      <td>May 21, 2010</td>
      <td>Shrek Forever After</td>
      <td>165000000.0</td>
      <td>238736787.0</td>
      <td>7.562447e+08</td>
      <td>5.912447e+08</td>
    </tr>
    <tr>
      <td>159</td>
      <td>60</td>
      <td>May 15, 2003</td>
      <td>The Matrix Reloaded</td>
      <td>150000000.0</td>
      <td>281553689.0</td>
      <td>7.385769e+08</td>
      <td>5.885769e+08</td>
    </tr>
    <tr>
      <td>2485</td>
      <td>86</td>
      <td>Nov 13, 1991</td>
      <td>Beauty and the Beast</td>
      <td>20000000.0</td>
      <td>376057266.0</td>
      <td>6.084311e+08</td>
      <td>5.884311e+08</td>
    </tr>
  </tbody>
</table>
<p>100 rows × 7 columns</p>
</div>




```python
#looking at the stats
display(df_tn_budget.describe())

#finding correlation
correlation = df.corr()
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
      <th>id</th>
      <th>production_budget</th>
      <th>domestic_gross</th>
      <th>worldwide_gross</th>
      <th>Profits</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>count</td>
      <td>5782.000000</td>
      <td>5.782000e+03</td>
      <td>5.782000e+03</td>
      <td>5.782000e+03</td>
      <td>5.782000e+03</td>
    </tr>
    <tr>
      <td>mean</td>
      <td>50.372363</td>
      <td>3.158776e+07</td>
      <td>4.187333e+07</td>
      <td>9.148746e+07</td>
      <td>5.989970e+07</td>
    </tr>
    <tr>
      <td>std</td>
      <td>28.821076</td>
      <td>4.181208e+07</td>
      <td>6.824060e+07</td>
      <td>1.747200e+08</td>
      <td>1.460889e+08</td>
    </tr>
    <tr>
      <td>min</td>
      <td>1.000000</td>
      <td>1.100000e+03</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>-2.002376e+08</td>
    </tr>
    <tr>
      <td>25%</td>
      <td>25.000000</td>
      <td>5.000000e+06</td>
      <td>1.429534e+06</td>
      <td>4.125415e+06</td>
      <td>-2.189071e+06</td>
    </tr>
    <tr>
      <td>50%</td>
      <td>50.000000</td>
      <td>1.700000e+07</td>
      <td>1.722594e+07</td>
      <td>2.798445e+07</td>
      <td>8.550286e+06</td>
    </tr>
    <tr>
      <td>75%</td>
      <td>75.000000</td>
      <td>4.000000e+07</td>
      <td>5.234866e+07</td>
      <td>9.764584e+07</td>
      <td>6.096850e+07</td>
    </tr>
    <tr>
      <td>max</td>
      <td>100.000000</td>
      <td>4.250000e+08</td>
      <td>9.366622e+08</td>
      <td>2.776345e+09</td>
      <td>2.351345e+09</td>
    </tr>
  </tbody>
</table>
</div>



```python
# dropping some columns
df = df_tn_budget.drop(['worldwide_gross', 'domestic_gross', 'id', 'movie','release_date'], axis = 1)
df.head()
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
      <th>production_budget</th>
      <th>Profits</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>425000000.0</td>
      <td>2.351345e+09</td>
    </tr>
    <tr>
      <td>42</td>
      <td>200000000.0</td>
      <td>2.008208e+09</td>
    </tr>
    <tr>
      <td>6</td>
      <td>300000000.0</td>
      <td>1.748134e+09</td>
    </tr>
    <tr>
      <td>5</td>
      <td>306000000.0</td>
      <td>1.747311e+09</td>
    </tr>
    <tr>
      <td>33</td>
      <td>215000000.0</td>
      <td>1.433855e+09</td>
    </tr>
  </tbody>
</table>
</div>




```python
budget_mean = df_tn_budget['production_budget'].mean()
round(budget_mean,3)
# $31,587,757
```




    31587757.097




```python
'https://dfrieds.com/data-visualizations/how-format-large-tick-values.html'

def reformat_large_tick_values(tick_val, pos):
    """
    Turns large tick values (in the billions, millions and thousands) such as 4500 into 4.5K and also appropriately turns 4000 into 4K (no zero after the decimal).
    """
    if tick_val >= 1000000000:
        val = round(tick_val/1000000000, 1)
        new_tick_format = '{:}B'.format(val)
    elif tick_val >= 1000000:
        val = round(tick_val/1000000, 1)
        new_tick_format = '{:}M'.format(val)
    elif tick_val >= 1000:
        val = round(tick_val/1000, 1)
        new_tick_format = '{:}K'.format(val)
    elif tick_val < 1000:
        new_tick_format = round(tick_val, 1)
    else:
        new_tick_format = tick_val

    # make new_tick_format into a string value
    new_tick_format = str(new_tick_format)
    
    # code below will keep 4.5M as is but change values such as 4.0M to 4M since that zero after the decimal isn't needed
    index_of_decimal = new_tick_format.find(".")
    
    if index_of_decimal != -1:
        value_after_decimal = new_tick_format[index_of_decimal+1]
        if value_after_decimal == "0":
            # remove the 0 after the decimal point since it's not needed
            new_tick_format = new_tick_format[0:index_of_decimal] + new_tick_format[index_of_decimal+2:]
            
    return new_tick_format
```


```python
import matplotlib
matplotlib.__version__
```




    '3.1.1'




```python
# new_figure = plt.figure(figsize=(20,10))
# ax = plt.axes()
# sns.barplot(data = df_tn_budget[:250], y= 'production_budget',
#             x = 'Profits',
#             ax=ax).set_title('Profits vs. Budget', fontsize = 25)
# # plt.xticks(rotation = 90)
# ax.set(xlabel = 'Production Budget')
# ax.xaxis.set_major_formatter(FuncFormatter(reformat_large_tick_values))
# ax.yaxis.set_major_formatter(FuncFormatter(reformat_large_tick_values));
```


```python
new_figure = plt.figure(figsize=(20,10))
ax = plt.axes()
sns.barplot(x= df_tn_budget['production_budget'][:250],
            y = df_tn_budget['Profits'][:250],
            ax=ax).set_title('Profits vs. Budget', fontsize = 25)
plt.xticks(rotation = 90)
ax.set(xlabel = 'Production Budget')
# ax.xaxis.set_major_formatter(FuncFormatter(reformat_large_tick_values))
ax.yaxis.set_major_formatter(FuncFormatter(reformat_large_tick_values));
# sns.regression(x= df_tn_budget['production_budget'][:250],y = df_tn_budget['Profits'][:250],ax=ax);
```


![png](output_48_0.png)



```python
new_figure = plt.figure(figsize=(10,7))
ax = plt.axes()
sns.regplot(x = 'production_budget', y = 'Profits', data = df_tn_budget, color = 'blue', line_kws = {'color':'green'}).set_title('Profits vs. Budget w/ Correlation')
plt.xticks(rotation = 90)
ax.set(xlabel = 'Production Budget')
ax.xaxis.set_major_formatter(FuncFormatter(reformat_large_tick_values))
ax.yaxis.set_major_formatter(FuncFormatter(reformat_large_tick_values));
```


![png](output_49_0.png)



```python
#correlation between profits and budget
corr = correlation['Profits'][0]
round(corr, 2)

```




    -0.0




```python
#Looking at where the common budget is usually spent at
new_figure = plt.figure(figsize=(10,5))
ax = plt.axes()
plt.hist(df_tn_budget['production_budget'], bins = 250)
plt.title('Distribution of Production Budgets')
plt.xlabel('Production Budget')
plt.ylabel('Number of Movies')
ax.xaxis.set_major_formatter(FuncFormatter(reformat_large_tick_values));
```


![png](output_51_0.png)


In the above graph we're able to look at the top 100 highest grossing movies of all time compared to their production budget. The production budget falls within the top 100. My recommendation to Microsoft, is to expect to pay $31,587,757 to yield the highest possibility of a profit.

## Most Profitable Month - Done


```python
df_tn_budget
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
      <th>id</th>
      <th>release_date</th>
      <th>movie</th>
      <th>production_budget</th>
      <th>domestic_gross</th>
      <th>worldwide_gross</th>
      <th>Profits</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>1</td>
      <td>Dec 18, 2009</td>
      <td>Avatar</td>
      <td>425000000.0</td>
      <td>760507625.0</td>
      <td>2.776345e+09</td>
      <td>2.351345e+09</td>
    </tr>
    <tr>
      <td>42</td>
      <td>43</td>
      <td>Dec 19, 1997</td>
      <td>Titanic</td>
      <td>200000000.0</td>
      <td>659363944.0</td>
      <td>2.208208e+09</td>
      <td>2.008208e+09</td>
    </tr>
    <tr>
      <td>6</td>
      <td>7</td>
      <td>Apr 27, 2018</td>
      <td>Avengers: Infinity War</td>
      <td>300000000.0</td>
      <td>678815482.0</td>
      <td>2.048134e+09</td>
      <td>1.748134e+09</td>
    </tr>
    <tr>
      <td>5</td>
      <td>6</td>
      <td>Dec 18, 2015</td>
      <td>Star Wars Ep. VII: The Force Awakens</td>
      <td>306000000.0</td>
      <td>936662225.0</td>
      <td>2.053311e+09</td>
      <td>1.747311e+09</td>
    </tr>
    <tr>
      <td>33</td>
      <td>34</td>
      <td>Jun 12, 2015</td>
      <td>Jurassic World</td>
      <td>215000000.0</td>
      <td>652270625.0</td>
      <td>1.648855e+09</td>
      <td>1.433855e+09</td>
    </tr>
    <tr>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <td>352</td>
      <td>53</td>
      <td>Apr 27, 2001</td>
      <td>Town &amp; Country</td>
      <td>105000000.0</td>
      <td>6712451.0</td>
      <td>1.036477e+07</td>
      <td>-9.463523e+07</td>
    </tr>
    <tr>
      <td>341</td>
      <td>42</td>
      <td>Jun 14, 2019</td>
      <td>Men in Black: International</td>
      <td>110000000.0</td>
      <td>3100000.0</td>
      <td>3.100000e+06</td>
      <td>-1.069000e+08</td>
    </tr>
    <tr>
      <td>193</td>
      <td>94</td>
      <td>Mar 11, 2011</td>
      <td>Mars Needs Moms</td>
      <td>150000000.0</td>
      <td>21392758.0</td>
      <td>3.954976e+07</td>
      <td>-1.104502e+08</td>
    </tr>
    <tr>
      <td>194</td>
      <td>95</td>
      <td>Dec 31, 2020</td>
      <td>Moonfall</td>
      <td>150000000.0</td>
      <td>0.0</td>
      <td>0.000000e+00</td>
      <td>-1.500000e+08</td>
    </tr>
    <tr>
      <td>2</td>
      <td>3</td>
      <td>Jun 7, 2019</td>
      <td>Dark Phoenix</td>
      <td>350000000.0</td>
      <td>42762350.0</td>
      <td>1.497624e+08</td>
      <td>-2.002376e+08</td>
    </tr>
  </tbody>
</table>
<p>5782 rows × 7 columns</p>
</div>




```python
#Converting to dates
df_tn_budget['release_date'] = pd.to_datetime(df_tn_budget['release_date'])
df_tn_budget.head()
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
      <th>id</th>
      <th>release_date</th>
      <th>movie</th>
      <th>production_budget</th>
      <th>domestic_gross</th>
      <th>worldwide_gross</th>
      <th>Profits</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>1</td>
      <td>2009-12-18</td>
      <td>Avatar</td>
      <td>425000000.0</td>
      <td>760507625.0</td>
      <td>2.776345e+09</td>
      <td>2.351345e+09</td>
    </tr>
    <tr>
      <td>42</td>
      <td>43</td>
      <td>1997-12-19</td>
      <td>Titanic</td>
      <td>200000000.0</td>
      <td>659363944.0</td>
      <td>2.208208e+09</td>
      <td>2.008208e+09</td>
    </tr>
    <tr>
      <td>6</td>
      <td>7</td>
      <td>2018-04-27</td>
      <td>Avengers: Infinity War</td>
      <td>300000000.0</td>
      <td>678815482.0</td>
      <td>2.048134e+09</td>
      <td>1.748134e+09</td>
    </tr>
    <tr>
      <td>5</td>
      <td>6</td>
      <td>2015-12-18</td>
      <td>Star Wars Ep. VII: The Force Awakens</td>
      <td>306000000.0</td>
      <td>936662225.0</td>
      <td>2.053311e+09</td>
      <td>1.747311e+09</td>
    </tr>
    <tr>
      <td>33</td>
      <td>34</td>
      <td>2015-06-12</td>
      <td>Jurassic World</td>
      <td>215000000.0</td>
      <td>652270625.0</td>
      <td>1.648855e+09</td>
      <td>1.433855e+09</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Creating a new columns called months and pulling just the months out of it
df_tn_budget["Month"] = pd.to_datetime(df_tn_budget['release_date'], format='%b', errors='coerce').dt.month
df_tn_budget.head()
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
      <th>id</th>
      <th>release_date</th>
      <th>movie</th>
      <th>production_budget</th>
      <th>domestic_gross</th>
      <th>worldwide_gross</th>
      <th>Profits</th>
      <th>Month</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>1</td>
      <td>2009-12-18</td>
      <td>Avatar</td>
      <td>425000000.0</td>
      <td>760507625.0</td>
      <td>2.776345e+09</td>
      <td>2.351345e+09</td>
      <td>12</td>
    </tr>
    <tr>
      <td>42</td>
      <td>43</td>
      <td>1997-12-19</td>
      <td>Titanic</td>
      <td>200000000.0</td>
      <td>659363944.0</td>
      <td>2.208208e+09</td>
      <td>2.008208e+09</td>
      <td>12</td>
    </tr>
    <tr>
      <td>6</td>
      <td>7</td>
      <td>2018-04-27</td>
      <td>Avengers: Infinity War</td>
      <td>300000000.0</td>
      <td>678815482.0</td>
      <td>2.048134e+09</td>
      <td>1.748134e+09</td>
      <td>4</td>
    </tr>
    <tr>
      <td>5</td>
      <td>6</td>
      <td>2015-12-18</td>
      <td>Star Wars Ep. VII: The Force Awakens</td>
      <td>306000000.0</td>
      <td>936662225.0</td>
      <td>2.053311e+09</td>
      <td>1.747311e+09</td>
      <td>12</td>
    </tr>
    <tr>
      <td>33</td>
      <td>34</td>
      <td>2015-06-12</td>
      <td>Jurassic World</td>
      <td>215000000.0</td>
      <td>652270625.0</td>
      <td>1.648855e+09</td>
      <td>1.433855e+09</td>
      <td>6</td>
    </tr>
  </tbody>
</table>
</div>




```python
#organizing months cronologically 
df_tn_budget.sort_values(by = 'Month', ascending = True, inplace = True)
```


```python
'https://stackoverflow.com/questions/37625334/python-pandas-convert-month-int-to-month-name'
#Getting the mean profits for each month
most_profitable_months = (df_tn_budget.groupby(df_tn_budget['Month'])['Profits'].mean())
most_profitable_months
```




    Month
    1     2.572033e+07
    2     4.349811e+07
    3     4.985129e+07
    4     3.611743e+07
    5     1.151328e+08
    6     9.942391e+07
    7     9.841746e+07
    8     3.542232e+07
    9     2.488078e+07
    10    2.907190e+07
    11    9.314157e+07
    12    6.844157e+07
    Name: Profits, dtype: float64




```python
#looking at when movies are typically released
plt.hist(df_tn_budget['Month'])
plt.title('Distribution of Release Months')
plt.xlabel('Month of the Year')
plt.ylabel('Number of Movies');
```


![png](output_59_0.png)



```python
# As we will see below, even though the most profitable months for movies is in May, 
# studios for some reason still release the majority of their films in December. 
# This could give us a competitive advantage
```


```python
# Putting names of month rather than the number
'https://stackoverflow.com/questions/37625334/python-pandas-convert-month-int-to-month-name'
import calendar
df_tn_budget['Month'] = df_tn_budget['Month'].apply(lambda x: calendar.month_abbr[x])
```


```python

```


```python
new_figure = plt.figure(figsize=(15,10))
ax = plt.axes()
sns.barplot(x = 'Month', y = 'Profits', data = df_tn_budget, ax=ax).set_title('Most Profitable Release Months')
plt.xticks(rotation = 90)
ax.yaxis.set_major_formatter(FuncFormatter(reformat_large_tick_values));
```


![png](output_63_0.png)


## Conclusions

There's a lot to take away from the above information. After looking at the distribution of budgets spent and months movies were most commonly released on, I'd recommend After releasing a film over the summer (May, June, July) in order to have the highest possible return.

I'd also recommend that Microsoft should expect to budget roughly $31MM in order to receive at least the average Profits (which are higher than the budget). 

My final recommendation is to have Microsoft focus within the adventure, animation and musical genres. These genres were the most profitable amongst the other genres. Think of movie studios like Disney, they hit all these markers with almost every movie they make, no wonder they're so successful.


```python

```

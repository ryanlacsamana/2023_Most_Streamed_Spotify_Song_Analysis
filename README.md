## **Analysis on the Most Streamed Spotify Songs 2023**

### **1. Introduction**

The dataset contains lists of the most streamed songs from the music streaming app **Spotify** for the year 2023. This dataset contains information for the track title, track artist(s), release date, musical ratings, BPM, musical keys, and streaming performance from other platforms such as Apple Music, Deezer, and Shazam. The numbers indicated in this dataset pertains to the values as of November 04, 2023, when this dataset was downloaded from [Kaggle](https://www.kaggle.com/datasets/nelgiriyewithana/top-spotify-songs-2023/data).

The dataset's summary of features are shown below:

Column Name | Description |
-----|-----|
track_name  |name of the song|
artist(s)_name |name of the artist(s) of the song|
artist_count |number of artists contributing to the song|
released_year   |year the song is released|
released_month  |month the song is released|
released_day    |day of the month the song is released|
in_spotify_playlists    |number of Spotify playlists the songs is included in|
in_spotify_charts   |presence and rank of the song in Spotify charts|
streams |total number of streams in Spotify|
in_apple_playlists    |number of Apple Music playlists the songs is included in|
in_apple_charts   |presence and rank of the song in Apple Music charts|
in_deezer_playlists    |number of Deezer playlists the songs is included in|
in_deezer_charts   |presence and rank of the song in Deezer charts|
in_shazam_charts   |presence and rank of the song in Shazam charts|
bpm |Beats per Minute, a measure of song tempo|
key |key of the song|
mode    |mode of the song (Major or Minor)|
danceability_%  |percentage indicating how suitable the song is for dancing|
valence_%   |positivity of the song's musical content|
energy_%    |perceived energy level of the song|
acousticness_%  |amount of acoustic sound in the song|
instrumentalness_%  |amount of instrumental content in the song|
liveness_%  |presence of live performance elements|
speechiness_%   |amount of spoken words in the song|



**Additional Notes for Musical Ratings**

- danceability_% - A value of 0 is least danceable, and 100 as most danceable.
- valence_% - Low valence sound more negative (e.g: sad, depressing, angry), while high valence sound more positive (e.g: happy, cheerful, euphoric)
- energy_% - Higher value sounds more energetic.
- acousticness_% - 100 represents high confidence the track is acoustic.
- instrumentalness_% - The closer the instrumentalness values is to 100, the greater likelihood the track contains no vocal content (ooh and aah sounds are treated as instrumental). Values above 50 are intended to represent instrumental tracks.
- liveness_% - higher liveness values represent an increased probability that the track is performed live. A value above 80 provides strong likelihood that the track is live.
- speechiness_% - Values above 66 describe tracks that are probably made entirely of spoken words. Values between 33 and 66 describe tracks that may contain both music and speech, including rap music.

### **1.1 Objectives**

1. Clean the data.
2. Identify relationship between variables.
3. Identify how the track metrics (danceability, energy, valence, acousticness, instrumentalness, liveness, and speechiness) relates to the number of streams, chart placement, and frequency in playlist of a certain track.
4. Share insights and findings through visualization and observations.

### **1.2 Methodology**

1. Create additional columns as necessary and modify values from certain columns to ease the analysis.
2. Check for null values and incorrect datatypes. Apply necessary measures to remove or replace these values.
3. Explore the data
4. Plot relationship between variables using visualization tools available in Seaborn and Matplotlib.
5. Write an observation based on the results of the analysis.
```
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import matplotlib.ticker as mticker
import seaborn as sns
import seaborn.objects as so

import warnings
warnings.simplefilter(action='ignore', category=FutureWarning)
```
```
df = pd.read_csv("D:\Documents\CSV Datasets\Spotify Songs\spotify-2023.csv", encoding='latin-1')
```

### **3. Data Preprocessing and Data Cleaning**

```
df.head(10)
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>track_name</th>
      <th>artist(s)_name</th>
      <th>artist_count</th>
      <th>released_year</th>
      <th>released_month</th>
      <th>released_day</th>
      <th>in_spotify_playlists</th>
      <th>in_spotify_charts</th>
      <th>streams</th>
      <th>in_apple_playlists</th>
      <th>...</th>
      <th>bpm</th>
      <th>key</th>
      <th>mode</th>
      <th>danceability_%</th>
      <th>valence_%</th>
      <th>energy_%</th>
      <th>acousticness_%</th>
      <th>instrumentalness_%</th>
      <th>liveness_%</th>
      <th>speechiness_%</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Seven (feat. Latto) (Explicit Ver.)</td>
      <td>Latto, Jung Kook</td>
      <td>2</td>
      <td>2023</td>
      <td>7</td>
      <td>14</td>
      <td>553</td>
      <td>147</td>
      <td>141381703</td>
      <td>43</td>
      <td>...</td>
      <td>125</td>
      <td>B</td>
      <td>Major</td>
      <td>80</td>
      <td>89</td>
      <td>83</td>
      <td>31</td>
      <td>0</td>
      <td>8</td>
      <td>4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>LALA</td>
      <td>Myke Towers</td>
      <td>1</td>
      <td>2023</td>
      <td>3</td>
      <td>23</td>
      <td>1474</td>
      <td>48</td>
      <td>133716286</td>
      <td>48</td>
      <td>...</td>
      <td>92</td>
      <td>C#</td>
      <td>Major</td>
      <td>71</td>
      <td>61</td>
      <td>74</td>
      <td>7</td>
      <td>0</td>
      <td>10</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>vampire</td>
      <td>Olivia Rodrigo</td>
      <td>1</td>
      <td>2023</td>
      <td>6</td>
      <td>30</td>
      <td>1397</td>
      <td>113</td>
      <td>140003974</td>
      <td>94</td>
      <td>...</td>
      <td>138</td>
      <td>F</td>
      <td>Major</td>
      <td>51</td>
      <td>32</td>
      <td>53</td>
      <td>17</td>
      <td>0</td>
      <td>31</td>
      <td>6</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Cruel Summer</td>
      <td>Taylor Swift</td>
      <td>1</td>
      <td>2019</td>
      <td>8</td>
      <td>23</td>
      <td>7858</td>
      <td>100</td>
      <td>800840817</td>
      <td>116</td>
      <td>...</td>
      <td>170</td>
      <td>A</td>
      <td>Major</td>
      <td>55</td>
      <td>58</td>
      <td>72</td>
      <td>11</td>
      <td>0</td>
      <td>11</td>
      <td>15</td>
    </tr>
    <tr>
      <th>4</th>
      <td>WHERE SHE GOES</td>
      <td>Bad Bunny</td>
      <td>1</td>
      <td>2023</td>
      <td>5</td>
      <td>18</td>
      <td>3133</td>
      <td>50</td>
      <td>303236322</td>
      <td>84</td>
      <td>...</td>
      <td>144</td>
      <td>A</td>
      <td>Minor</td>
      <td>65</td>
      <td>23</td>
      <td>80</td>
      <td>14</td>
      <td>63</td>
      <td>11</td>
      <td>6</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Sprinter</td>
      <td>Dave, Central Cee</td>
      <td>2</td>
      <td>2023</td>
      <td>6</td>
      <td>1</td>
      <td>2186</td>
      <td>91</td>
      <td>183706234</td>
      <td>67</td>
      <td>...</td>
      <td>141</td>
      <td>C#</td>
      <td>Major</td>
      <td>92</td>
      <td>66</td>
      <td>58</td>
      <td>19</td>
      <td>0</td>
      <td>8</td>
      <td>24</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Ella Baila Sola</td>
      <td>Eslabon Armado, Peso Pluma</td>
      <td>2</td>
      <td>2023</td>
      <td>3</td>
      <td>16</td>
      <td>3090</td>
      <td>50</td>
      <td>725980112</td>
      <td>34</td>
      <td>...</td>
      <td>148</td>
      <td>F</td>
      <td>Minor</td>
      <td>67</td>
      <td>83</td>
      <td>76</td>
      <td>48</td>
      <td>0</td>
      <td>8</td>
      <td>3</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Columbia</td>
      <td>Quevedo</td>
      <td>1</td>
      <td>2023</td>
      <td>7</td>
      <td>7</td>
      <td>714</td>
      <td>43</td>
      <td>58149378</td>
      <td>25</td>
      <td>...</td>
      <td>100</td>
      <td>F</td>
      <td>Major</td>
      <td>67</td>
      <td>26</td>
      <td>71</td>
      <td>37</td>
      <td>0</td>
      <td>11</td>
      <td>4</td>
    </tr>
    <tr>
      <th>8</th>
      <td>fukumean</td>
      <td>Gunna</td>
      <td>1</td>
      <td>2023</td>
      <td>5</td>
      <td>15</td>
      <td>1096</td>
      <td>83</td>
      <td>95217315</td>
      <td>60</td>
      <td>...</td>
      <td>130</td>
      <td>C#</td>
      <td>Minor</td>
      <td>85</td>
      <td>22</td>
      <td>62</td>
      <td>12</td>
      <td>0</td>
      <td>28</td>
      <td>9</td>
    </tr>
    <tr>
      <th>9</th>
      <td>La Bebe - Remix</td>
      <td>Peso Pluma, Yng Lvcas</td>
      <td>2</td>
      <td>2023</td>
      <td>3</td>
      <td>17</td>
      <td>2953</td>
      <td>44</td>
      <td>553634067</td>
      <td>49</td>
      <td>...</td>
      <td>170</td>
      <td>D</td>
      <td>Minor</td>
      <td>81</td>
      <td>56</td>
      <td>48</td>
      <td>21</td>
      <td>0</td>
      <td>8</td>
      <td>33</td>
    </tr>
  </tbody>
</table>
<p>10 rows × 24 columns</p>
</div>

```
df.info()
```
```
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 953 entries, 0 to 952
Data columns (total 24 columns):
 #   Column                Non-Null Count  Dtype 
---  ------                --------------  ----- 
 0   track_name            953 non-null    object
 1   artist(s)_name        953 non-null    object
 2   artist_count          953 non-null    int64 
 3   released_year         953 non-null    int64 
 4   released_month        953 non-null    int64 
 5   released_day          953 non-null    int64 
 6   in_spotify_playlists  953 non-null    int64 
 7   in_spotify_charts     953 non-null    int64 
 8   streams               953 non-null    object
 9   in_apple_playlists    953 non-null    int64 
 10  in_apple_charts       953 non-null    int64 
 11  in_deezer_playlists   953 non-null    object
 12  in_deezer_charts      953 non-null    int64 
 13  in_shazam_charts      903 non-null    object
 14  bpm                   953 non-null    int64 
 15  key                   858 non-null    object
 16  mode                  953 non-null    object
 17  danceability_%        953 non-null    int64 
 18  valence_%             953 non-null    int64 
 19  energy_%              953 non-null    int64 
 20  acousticness_%        953 non-null    int64 
 21  instrumentalness_%    953 non-null    int64 
 22  liveness_%            953 non-null    int64 
 23  speechiness_%         953 non-null    int64 
dtypes: int64(17), object(7)
memory usage: 178.8+ KB
```
```
print(df.isnull().sum())
```
```
track_name               0
artist(s)_name           0
artist_count             0
released_year            0
released_month           0
released_day             0
in_spotify_playlists     0
in_spotify_charts        0
streams                  0
in_apple_playlists       0
in_apple_charts          0
in_deezer_playlists      0
in_deezer_charts         0
in_shazam_charts        50
bpm                      0
key                     95
mode                     0
danceability_%           0
valence_%                0
energy_%                 0
acousticness_%           0
instrumentalness_%       0
liveness_%               0
speechiness_%            0
dtype: int64
```
#### **3.1 Checking of Values in the Dataset**

#### 3.1.1 Null values

- The dataset contains null values from the columns **`in_shazam_charts`** and **`key`**. For the null values in the **`in_shazam_charts`** column, it is possible that these songs have the most number of streams but did not hit the charts in Shazam. 
- For the null values in the **`key`** column, based on [Spotify for Developers - Get Track's Audio Features](https://developer.spotify.com/documentation/web-api/reference/get-audio-features), the key of the song can be converted into **integers** using the standard [Pitch Class Notation](https://en.wikipedia.org/wiki/Pitch_class). The null values for the `key` column will have a value of **-1**.

#### 3.1.2 Incorrect datatypes

- The following columns have incorrect datatypes:
  - streams
  - in_deezer_playlists
  - in_shazam_charts
  
  The datatype for these columns will be converted into **int64.**

#### 3.1.3 Pitch Class Notation

Pitch Class | Tonal Counterparts |
-----|-----|
0 |C  |
1 |C# |
2 |D  |
3 |D# |
4 |E  |
5 |F  |
6 |F# |
7 |G  |
8 |G# |
9 |A  |
10  |A# |
11  |B  |

#### 3.1.4 Additional Column

- A new column will be created to classify a track's placement in the charts. There will four (4) additional columns with the following metrics for rating a track's placement:
  - 0                 - Uncharted
  - 1 - 10            - Top 10
  - 11 - 50           - Top 50
  - 51 - 100          - Top 100
  - 101 - 200         - Top 200
  - Greater than 200  - Charted
```
## Replace null values in 'in_shazam_charts' column into 0
df['in_shazam_charts'].fillna(0, inplace=True)

## Replace invalid data in the 'stream' column into null
df['streams'] = df['streams'] = pd.to_numeric(df['streams'], errors='coerce')

## Replace null values in 'key' column into 'none'
df['key'] = df['key'].fillna(-1)
```
```
## Drop the null value in the 'streams' column
df = df.dropna(how='any')

print(df.isnull().sum())
```
```
track_name              0
artist(s)_name          0
artist_count            0
released_year           0
released_month          0
released_day            0
in_spotify_playlists    0
in_spotify_charts       0
streams                 0
in_apple_playlists      0
in_apple_charts         0
in_deezer_playlists     0
in_deezer_charts        0
in_shazam_charts        0
bpm                     0
key                     0
mode                    0
danceability_%          0
valence_%               0
energy_%                0
acousticness_%          0
instrumentalness_%      0
liveness_%              0
speechiness_%           0
dtype: int64
```
```
## Remove the comma (,) for some values in columns 'in_deezer_playlists' and 'in_shazam_charts' and convert them into int64
df['in_deezer_playlists'] = df['in_deezer_playlists'].replace(',', '', regex=True).astype('int64')
df['in_shazam_charts'] = df['in_shazam_charts'].replace(',', '', regex=True).astype('int64')

## Change the datatype of 'streams' column into int64
df['streams'] = df['streams'].astype('int64')
```
```
## Change values in 'key' column into integers using Pitch Class Notation
pitch_class = {'C': 0,
               'C#': 1,
               'D': 2,
               'D#': 3,
               'E': 4,
               'F': 5,
               'F#': 6,
               'G': 7,
               'G#': 8,
               'A': 9,
               'A#': 10,
               'B': 11
               }

df['key'] = df['key'].map(pitch_class).fillna(-1)
```
```
## Create new columns for track's chart classification
def chart_cat(value):
    if value == 0:
        return 'Uncharted'
    elif 1 <= value <= 10:
        return 'Top 10'
    elif 11 <= value <= 50:
        return 'Top 50'
    elif 51 <= value <= 100:
        return 'Top 100'
    elif 101 <= value <= 200:
        return 'Top 200'
    else:
        return 'Charted'
    
for col_chart in ['in_spotify_charts','in_apple_charts','in_deezer_charts','in_shazam_charts']:
    new_col_chart_name = col_chart + '_category'
    df[new_col_chart_name] = df[col_chart].apply(chart_cat)
```
```
df.head()
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>track_name</th>
      <th>artist(s)_name</th>
      <th>artist_count</th>
      <th>released_year</th>
      <th>released_month</th>
      <th>released_day</th>
      <th>in_spotify_playlists</th>
      <th>in_spotify_charts</th>
      <th>streams</th>
      <th>in_apple_playlists</th>
      <th>...</th>
      <th>valence_%</th>
      <th>energy_%</th>
      <th>acousticness_%</th>
      <th>instrumentalness_%</th>
      <th>liveness_%</th>
      <th>speechiness_%</th>
      <th>in_spotify_charts_category</th>
      <th>in_apple_charts_category</th>
      <th>in_deezer_charts_category</th>
      <th>in_shazam_charts_category</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Seven (feat. Latto) (Explicit Ver.)</td>
      <td>Latto, Jung Kook</td>
      <td>2</td>
      <td>2023</td>
      <td>7</td>
      <td>14</td>
      <td>553</td>
      <td>147</td>
      <td>141381703</td>
      <td>43</td>
      <td>...</td>
      <td>89</td>
      <td>83</td>
      <td>31</td>
      <td>0</td>
      <td>8</td>
      <td>4</td>
      <td>Top 200</td>
      <td>Charted</td>
      <td>Top 10</td>
      <td>Charted</td>
    </tr>
    <tr>
      <th>1</th>
      <td>LALA</td>
      <td>Myke Towers</td>
      <td>1</td>
      <td>2023</td>
      <td>3</td>
      <td>23</td>
      <td>1474</td>
      <td>48</td>
      <td>133716286</td>
      <td>48</td>
      <td>...</td>
      <td>61</td>
      <td>74</td>
      <td>7</td>
      <td>0</td>
      <td>10</td>
      <td>4</td>
      <td>Top 50</td>
      <td>Top 200</td>
      <td>Top 50</td>
      <td>Charted</td>
    </tr>
    <tr>
      <th>2</th>
      <td>vampire</td>
      <td>Olivia Rodrigo</td>
      <td>1</td>
      <td>2023</td>
      <td>6</td>
      <td>30</td>
      <td>1397</td>
      <td>113</td>
      <td>140003974</td>
      <td>94</td>
      <td>...</td>
      <td>32</td>
      <td>53</td>
      <td>17</td>
      <td>0</td>
      <td>31</td>
      <td>6</td>
      <td>Top 200</td>
      <td>Charted</td>
      <td>Top 50</td>
      <td>Charted</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Cruel Summer</td>
      <td>Taylor Swift</td>
      <td>1</td>
      <td>2019</td>
      <td>8</td>
      <td>23</td>
      <td>7858</td>
      <td>100</td>
      <td>800840817</td>
      <td>116</td>
      <td>...</td>
      <td>58</td>
      <td>72</td>
      <td>11</td>
      <td>0</td>
      <td>11</td>
      <td>15</td>
      <td>Top 100</td>
      <td>Charted</td>
      <td>Top 50</td>
      <td>Charted</td>
    </tr>
    <tr>
      <th>4</th>
      <td>WHERE SHE GOES</td>
      <td>Bad Bunny</td>
      <td>1</td>
      <td>2023</td>
      <td>5</td>
      <td>18</td>
      <td>3133</td>
      <td>50</td>
      <td>303236322</td>
      <td>84</td>
      <td>...</td>
      <td>23</td>
      <td>80</td>
      <td>14</td>
      <td>63</td>
      <td>11</td>
      <td>6</td>
      <td>Top 50</td>
      <td>Top 200</td>
      <td>Top 50</td>
      <td>Charted</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 28 columns</p>
</div>

```
df.info()
```
```
<class 'pandas.core.frame.DataFrame'>
Index: 952 entries, 0 to 952
Data columns (total 28 columns):
 #   Column                      Non-Null Count  Dtype 
---  ------                      --------------  ----- 
 0   track_name                  952 non-null    object
 1   artist(s)_name              952 non-null    object
 2   artist_count                952 non-null    int64 
 3   released_year               952 non-null    int64 
 4   released_month              952 non-null    int64 
 5   released_day                952 non-null    int64 
 6   in_spotify_playlists        952 non-null    int64 
 7   in_spotify_charts           952 non-null    int64 
 8   streams                     952 non-null    int64 
 9   in_apple_playlists          952 non-null    int64 
 10  in_apple_charts             952 non-null    int64 
 11  in_deezer_playlists         952 non-null    int64 
 12  in_deezer_charts            952 non-null    int64 
 13  in_shazam_charts            952 non-null    int64 
 14  bpm                         952 non-null    int64 
 15  key                         952 non-null    int64 
 16  mode                        952 non-null    object
 17  danceability_%              952 non-null    int64 
 18  valence_%                   952 non-null    int64 
 19  energy_%                    952 non-null    int64 
 20  acousticness_%              952 non-null    int64 
 21  instrumentalness_%          952 non-null    int64 
 22  liveness_%                  952 non-null    int64 
 23  speechiness_%               952 non-null    int64 
 24  in_spotify_charts_category  952 non-null    object
 25  in_apple_charts_category    952 non-null    object
 26  in_deezer_charts_category   952 non-null    object
 27  in_shazam_charts_category   952 non-null    object
dtypes: int64(21), object(7)
memory usage: 215.7+ KB
```

#### **3.2 Descriptive Statistics**

```
df.describe()
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>artist_count</th>
      <th>released_year</th>
      <th>released_month</th>
      <th>released_day</th>
      <th>in_spotify_playlists</th>
      <th>in_spotify_charts</th>
      <th>streams</th>
      <th>in_apple_playlists</th>
      <th>in_apple_charts</th>
      <th>in_deezer_playlists</th>
      <th>...</th>
      <th>in_shazam_charts</th>
      <th>bpm</th>
      <th>key</th>
      <th>danceability_%</th>
      <th>valence_%</th>
      <th>energy_%</th>
      <th>acousticness_%</th>
      <th>instrumentalness_%</th>
      <th>liveness_%</th>
      <th>speechiness_%</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>952.000000</td>
      <td>952.000000</td>
      <td>952.000000</td>
      <td>952.000000</td>
      <td>952.000000</td>
      <td>952.000000</td>
      <td>9.520000e+02</td>
      <td>952.000000</td>
      <td>952.000000</td>
      <td>952.000000</td>
      <td>...</td>
      <td>952.000000</td>
      <td>952.000000</td>
      <td>952.000000</td>
      <td>952.000000</td>
      <td>952.000000</td>
      <td>952.000000</td>
      <td>952.000000</td>
      <td>952.000000</td>
      <td>952.000000</td>
      <td>952.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>1.556723</td>
      <td>2018.288866</td>
      <td>6.038866</td>
      <td>13.944328</td>
      <td>5202.565126</td>
      <td>12.022059</td>
      <td>5.141374e+08</td>
      <td>67.866597</td>
      <td>51.963235</td>
      <td>385.535714</td>
      <td>...</td>
      <td>56.907563</td>
      <td>122.553571</td>
      <td>5.193277</td>
      <td>66.984244</td>
      <td>51.406513</td>
      <td>64.274160</td>
      <td>27.078782</td>
      <td>1.582983</td>
      <td>18.214286</td>
      <td>10.138655</td>
    </tr>
    <tr>
      <th>std</th>
      <td>0.893331</td>
      <td>11.011397</td>
      <td>3.564571</td>
      <td>9.197223</td>
      <td>7901.400683</td>
      <td>19.582405</td>
      <td>5.668569e+08</td>
      <td>86.470591</td>
      <td>50.628850</td>
      <td>1131.078760</td>
      <td>...</td>
      <td>157.513706</td>
      <td>28.069601</td>
      <td>3.701314</td>
      <td>14.631282</td>
      <td>23.480526</td>
      <td>16.558517</td>
      <td>26.001599</td>
      <td>8.414064</td>
      <td>13.718374</td>
      <td>9.915399</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1.000000</td>
      <td>1930.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>31.000000</td>
      <td>0.000000</td>
      <td>2.762000e+03</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>...</td>
      <td>0.000000</td>
      <td>65.000000</td>
      <td>-1.000000</td>
      <td>23.000000</td>
      <td>4.000000</td>
      <td>9.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>3.000000</td>
      <td>2.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>1.000000</td>
      <td>2020.000000</td>
      <td>3.000000</td>
      <td>6.000000</td>
      <td>874.500000</td>
      <td>0.000000</td>
      <td>1.416362e+08</td>
      <td>13.000000</td>
      <td>7.000000</td>
      <td>13.000000</td>
      <td>...</td>
      <td>0.000000</td>
      <td>99.750000</td>
      <td>2.000000</td>
      <td>57.000000</td>
      <td>32.000000</td>
      <td>53.000000</td>
      <td>6.000000</td>
      <td>0.000000</td>
      <td>10.000000</td>
      <td>4.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>1.000000</td>
      <td>2022.000000</td>
      <td>6.000000</td>
      <td>13.000000</td>
      <td>2216.500000</td>
      <td>3.000000</td>
      <td>2.905309e+08</td>
      <td>34.000000</td>
      <td>38.500000</td>
      <td>44.000000</td>
      <td>...</td>
      <td>2.000000</td>
      <td>121.000000</td>
      <td>5.000000</td>
      <td>69.000000</td>
      <td>51.000000</td>
      <td>66.000000</td>
      <td>18.000000</td>
      <td>0.000000</td>
      <td>12.000000</td>
      <td>6.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>2.000000</td>
      <td>2022.000000</td>
      <td>9.000000</td>
      <td>22.000000</td>
      <td>5573.750000</td>
      <td>16.000000</td>
      <td>6.738690e+08</td>
      <td>88.000000</td>
      <td>87.000000</td>
      <td>164.250000</td>
      <td>...</td>
      <td>33.250000</td>
      <td>140.250000</td>
      <td>8.000000</td>
      <td>78.000000</td>
      <td>70.000000</td>
      <td>77.000000</td>
      <td>43.000000</td>
      <td>0.000000</td>
      <td>24.000000</td>
      <td>11.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>8.000000</td>
      <td>2023.000000</td>
      <td>12.000000</td>
      <td>31.000000</td>
      <td>52898.000000</td>
      <td>147.000000</td>
      <td>3.703895e+09</td>
      <td>672.000000</td>
      <td>275.000000</td>
      <td>12367.000000</td>
      <td>...</td>
      <td>1451.000000</td>
      <td>206.000000</td>
      <td>11.000000</td>
      <td>96.000000</td>
      <td>97.000000</td>
      <td>97.000000</td>
      <td>97.000000</td>
      <td>91.000000</td>
      <td>97.000000</td>
      <td>64.000000</td>
    </tr>
  </tbody>
</table>
<p>8 rows × 21 columns</p>
</div>

**Observations:**

Release Date

- The year of release of the latest song in the dataset is (of course) **2023**, with the oldest dating back to **1930**.

Popularity

- Some of the most streamed songs never landed in the charts.
- The most number of streams is **3,703,895,000**, while the least number of streams is **2,762**.
- The mean number of streams is **514,137,400** with a standard deviation of **566,856,900**, which indicates that the number of streams varies by a huge value.

Song Properties / Characteristics

- The highest and lowest BPM is **206** and **65**, respectively, with a mean value of **122.55**.
- The highest and lowest danceability is 96% and 23%, respectively, with a mean value of 66.98%.
- The highest and lowest valence is 97% and 4%, respectively, with a mean value of 51.41%.
- The highest and lowest energy is 97% and 9%, repectively, with a mean value of 64.27%.
- The highest and lowest acousticness is 97% and 0%, respectively, with a mean value of 27.08%.
- The highest and lowest instrumentalness is 91% and 0%, respectively, with a mean value of 1.58%.
- The highest and lowest liveness is 97% and 3%, respectively, with a mean value of 18.21%.
- The highest and lowest speechiness is 64% and 2%, respectively, with a mean value of 10.14%.

### **4. Data Visualization**

### 4.1 Most Streamed Songs

```
## Sort the data based on the number of streams in descending order
df_sorted = df.sort_values(by='streams', ascending=False)

top_10_streamed = df_sorted.head(10)
```
```
## Create a bar chart to visualize the top 10 most streamed songs
plt.subplots(1,1, figsize=(6,4))

sns.barplot(data=top_10_streamed, x='streams', y='track_name')
plt.xlabel('Streams (in billions)', fontsize=7)
plt.ylabel('Track Name', fontsize=7)
plt.xticks(rotation=45, fontsize=7)
plt.yticks(fontsize=7)

plt.show()
```
![image](https://github.com/ryanlacsamana/2023_Most_Streamed_Spotify_Song_Analysis/assets/138304188/1f07b392-7264-4aee-a8f7-2f9cace49917)

### 4.2 Relationship between Stream Count and other Variables

```
## Create a dataset to only include columns with numeric variables
df_int = df.select_dtypes(include='int64').copy()

## Drop the 'released_month' and 'released_day' columns as we will only analyze the data based on 'released_year'
df_int = df_int.drop(columns=['released_month','released_day'])

df_int.head()
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>artist_count</th>
      <th>released_year</th>
      <th>in_spotify_playlists</th>
      <th>in_spotify_charts</th>
      <th>streams</th>
      <th>in_apple_playlists</th>
      <th>in_apple_charts</th>
      <th>in_deezer_playlists</th>
      <th>in_deezer_charts</th>
      <th>in_shazam_charts</th>
      <th>bpm</th>
      <th>key</th>
      <th>danceability_%</th>
      <th>valence_%</th>
      <th>energy_%</th>
      <th>acousticness_%</th>
      <th>instrumentalness_%</th>
      <th>liveness_%</th>
      <th>speechiness_%</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2</td>
      <td>2023</td>
      <td>553</td>
      <td>147</td>
      <td>141381703</td>
      <td>43</td>
      <td>263</td>
      <td>45</td>
      <td>10</td>
      <td>826</td>
      <td>125</td>
      <td>11</td>
      <td>80</td>
      <td>89</td>
      <td>83</td>
      <td>31</td>
      <td>0</td>
      <td>8</td>
      <td>4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>2023</td>
      <td>1474</td>
      <td>48</td>
      <td>133716286</td>
      <td>48</td>
      <td>126</td>
      <td>58</td>
      <td>14</td>
      <td>382</td>
      <td>92</td>
      <td>1</td>
      <td>71</td>
      <td>61</td>
      <td>74</td>
      <td>7</td>
      <td>0</td>
      <td>10</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>2023</td>
      <td>1397</td>
      <td>113</td>
      <td>140003974</td>
      <td>94</td>
      <td>207</td>
      <td>91</td>
      <td>14</td>
      <td>949</td>
      <td>138</td>
      <td>5</td>
      <td>51</td>
      <td>32</td>
      <td>53</td>
      <td>17</td>
      <td>0</td>
      <td>31</td>
      <td>6</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>2019</td>
      <td>7858</td>
      <td>100</td>
      <td>800840817</td>
      <td>116</td>
      <td>207</td>
      <td>125</td>
      <td>12</td>
      <td>548</td>
      <td>170</td>
      <td>9</td>
      <td>55</td>
      <td>58</td>
      <td>72</td>
      <td>11</td>
      <td>0</td>
      <td>11</td>
      <td>15</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>2023</td>
      <td>3133</td>
      <td>50</td>
      <td>303236322</td>
      <td>84</td>
      <td>133</td>
      <td>87</td>
      <td>15</td>
      <td>425</td>
      <td>144</td>
      <td>9</td>
      <td>65</td>
      <td>23</td>
      <td>80</td>
      <td>14</td>
      <td>63</td>
      <td>11</td>
      <td>6</td>
    </tr>
  </tbody>
</table>
</div>

```
## Plot a histogram to visualize the descriptive statistics of each variable
plt.figure(figsize=(25,20))

for i, col in enumerate(df_int.columns):
    plt.subplot(5,4, i+1)
    sns.histplot(data=df_int, x=col, bins=10, kde=True)
    plt.tight_layout
    
plt.show()
```

![image](https://github.com/ryanlacsamana/2023_Most_Streamed_Spotify_Song_Analysis/assets/138304188/7b0deec3-67b8-4da1-9594-fb7dca61a4a7)

```
## Plot a scatterplot to visualize the spread of variables and its relationship to the stream count
plt.figure(figsize=(25,20))

int_no_stream = [col for col in df_int.columns
                   if col != 'streams']

for i, col in enumerate(int_no_stream):
    plt.subplot(5,4, i+1)
    sns.scatterplot(data=df_int, x=col, y='streams')
    
plt.tight_layout()
plt.show()
```

![image](https://github.com/ryanlacsamana/2023_Most_Streamed_Spotify_Song_Analysis/assets/138304188/8fbf610f-e53a-4f2c-8c76-9d1fab59df51)

```
## Create a boxplot for total stream duration vs chart placement category
fig, ax = plt.subplots(1,4, figsize=(20,5))

sns.set(font_scale = 0.9)
custom_order = ['Uncharted','Top 10','Top 50','Top 100','Top 200','Charted']

## For Spotify charts
sns.boxplot(data=df, x='streams', y='in_spotify_charts_category', order=custom_order, palette=sns.color_palette('hls'), width=0.3, fliersize=2, ax=ax[0])
ax[0].legend([])
ax[0].set_xlabel(xlabel='total stream duration')
## For Apple charts
sns.boxplot(data=df, x='streams', y='in_apple_charts_category', order=custom_order, palette=sns.color_palette('hls'), width=0.3, fliersize=2, ax=ax[1])
ax[1].legend([])
ax[1].set_xlabel(xlabel='total stream duration')
## For Deezer charts
sns.boxplot(data=df, x='streams', y='in_deezer_charts_category', order=custom_order, palette=sns.color_palette('hls'), width=0.3, fliersize=2, ax=ax[2])
ax[2].legend([])
ax[2].set_xlabel(xlabel='total stream duration')
## For Shazam charts
sns.boxplot(data=df, x='streams', y='in_shazam_charts_category', order=custom_order, palette=sns.color_palette('hls'), width=0.3, fliersize=2, ax=ax[3])
ax[3].legend([])
ax[3].set_xlabel(xlabel='total stream duration')

plt.tight_layout()
plt.show()
```

![image](https://github.com/ryanlacsamana/2023_Most_Streamed_Spotify_Song_Analysis/assets/138304188/5c9808a5-7fd1-4eb9-9a8a-751d21c46c23)

#### 4.2.1 Observations

**1. Artist Count**
   - Tracks with only 1 artist seem to be more popular and streamed more.
  
**2. Year of Release**
   - Newer songs tend to be streamed more, as shown in both the histogram and scatterplot, but older songs that dates back up to 1930 received a lot of streaming too.
   - The older songs that received a lot of streaming could be classic songs, or songs that were brought back to popularity due to some usage in social media.

**3. Presence in Platform Playlists**
   - The histogram for `in_spotify_playlists`, `in_apple_playlists`, and `in_deezer_playlists` are all skewed to the left. The scatterplot for these columns also shows that huge number of tracks populate the lower values. This means that most of the top streamed songs are not included in the subscriber's playlist.
   - These findings, combined with the findings for the `released_year` column could mean that these top streamed songs are new songs, which typically receives a lot of streaming, or which have not yet been added to most playlist. This could also mean that the number of streaming a track receives does not necessarily mean a subscriber will like them.

**4. Presence in Platform Charts**
   - The histogram for `in_spotify_charts`, `in_apple_charts`, `in_deezer_charts`, and `in_shazam_charts` are also skewed to the left. However, since the values for the charts indicate that the lower numbers indicate a higher placement in the charts, or a value of zero means that a track does not place in a chart, the histograms and scatterplots are not enough to visualize the relationship, hence, the creation of new columns for chart classification.
   - There are top streamed songs that did not place in a chart for both Spotify and Deezer.
   - Uncharted tracks have shorter total streaming duration for Spotify, Deezer, and Shazam, however, the tracks that placed in the Top 10 charts have the shortest total streaming duration in Apple.
   - The tracks in Spotify that placed within the top 101 to 200 in Spotify received a largely varying streaming time, having both tracks that has the one of the lowest and the highest streaming duration, and the highest interquartile range.

**5. BPM**
   - The BPM with the most streamed music is 120, with 90 BPM follows closely. Tracks with high BPM values have few number of streams.
   - Listeners prefer to stream music with moderate speed.

**6. Key**
   - There are no streamed music with the key 0 (C).
   - The music key with the most streams is 1 (C#), while the least is 3 (D#).
   - The amount of streams for the other keys have small variations.

**7. Track Metrics**
   - **7.1 Danceability**
     - Listeners stream more to danceable tracks, as shown in the histogram with the highest amount of streams in 70%.
   - **7.2 Valence**
     - The highest amount of stream is at the 50% valence. The number of tracks and amount of streams seem to vary only in small amounts as the valence value increases or decreases from 50%.
     - This findings could mean that the mood of the top streamed songs is neutral, as it includes songs from different types of moods.
   - **7.3 Energy**
     - The most number of streams are also at the 70% energy value. This could be related to listeners preference to danceable tracks.
   - **7.4 Acousticness**
     - The histogram shows a left-skewed plot, which means that a considerable amount of top streamed songs are not acoustic.
     - In the scatterplot, however, the findings seem to be not biased to non-acoustic songs, as some points still populate the chart in the higher acoustic levels, with the most time of streaming present in the higher levels.
     - Based on this findings, tracks that are partially acoustic gain more listening time compared to non-acoustic tracks. It is only the large amount of non-acoustic tracks that contribute to the large amount of streaming time.
   - **7.5 Instrumentalness**
     - The histogram and scatterplot both show that listeners prefer to listen to tracks that have both music and singing, as the plot is skewed to the left and populates in the lowest values of instrumentalness.
   - **7.6 Liveness**
     - The histogram and scatterplot both show that listeners prefer to listen to recorded tracks, as the plot is skewed to the left and populates in the lower values of liveness.
   - **7.7 Speechiness**
     - The histogram and scatterplot both show that listeners prefer to listen to tracks with more singing than speech.
    
### 4.3 Correlation Matrix

After checking the histograms, scatterplots, and boxplots for the relationship between variables and stream count, we will plot a heatmap correlating variables that could have high correlation to the number of streams.

```
## Plot a correlation matrix
col_to_corr = ['artist_count','released_year','in_spotify_playlists','in_spotify_charts','streams','in_apple_playlists','in_apple_charts','in_deezer_playlists','in_deezer_charts',
               'in_shazam_charts','danceability_%','valence_%','energy_%','acousticness_%','instrumentalness_%','liveness_%','speechiness_%']

corr_matrix = df_int[col_to_corr].corr()
mask = np.triu(corr_matrix, k=1)
mask = mask | (corr_matrix >= 0.5)

plt.figure(figsize=(12,10))
sns.heatmap(corr_matrix, annot=True, fmt='.2f', square=True, mask=~mask, cmap='coolwarm')
sns.set(font_scale=0.7)

plt.show()
```

![image](https://github.com/ryanlacsamana/2023_Most_Streamed_Spotify_Song_Analysis/assets/138304188/474915c7-66cf-4a5a-8126-425359addc50)

Based on the correlation heatmap, the values in the columns `in_spotify_playlists` and `in_apple_playlists` have high correlation to the number of streams, with correlation values more than 0.70. Values in the `in_deezer_playlists` have a moderate to good correlation to the number of streams with a value of more than 0.50.

### 4.4 Analysis of the Distribution of Track Metrics per Year of Release

#### **4.4.1 Danceability**

```
## Create a boxplot
plt.subplots(1,1, figsize=(15,3))

sns.boxplot(data=df, x='released_year', y='danceability_%', width=0.4, fliersize=2)
plt.xticks(rotation=45, fontsize=8)

plt.show()
```

![image](https://github.com/ryanlacsamana/2023_Most_Streamed_Spotify_Song_Analysis/assets/138304188/1cc29687-e9d0-4087-8766-7b8521f95e6b)

- Tracks that are released from the year 2020 to 2023 have almost similar median danceability, and almost similar interquartile range.
- Tracks that are released from 2008 to 2023 have wide range of danceability. It could be due to the majority of the top tracks were released in these years.
- The most danceable track in the top streamed songs was released in 2021.
- The least danceable track in the top streamed songs was released in 1942.

#### **4.4.2 Valence**
```
## Create a boxplot
plt.subplots(1,1, figsize=(15,3))

sns.boxplot(data=df, x='released_year', y='valence_%', width=0.4, fliersize=2)
plt.xticks(rotation=45, fontsize=8)

plt.show()
```

![image](https://github.com/ryanlacsamana/2023_Most_Streamed_Spotify_Song_Analysis/assets/138304188/5b9f2cf5-da3f-47c1-aa96-aba287d0ed89)

- Tracks from 2020 to 2023 shows wide variety of moods in the top streamed songs, long whiskers extending from low valence to high valence, and median values at approximately 50%.
- Tracks from 2011 to 2023 has median valence at approximately 40 to 50%, with the exception of 2018. The range is also at the middle of the chart, ranging 20 to 70%, which shows the neutrality of the mood in the top streamed songs.

#### **4.4.3 Energy**

```
## Create a boxplot
plt.subplots(1,1, figsize=(15,3))

sns.boxplot(data=df, x='released_year', y='energy_%', width=0.4, fliersize=2)
plt.xticks(rotation=45, fontsize=8)

plt.show()
```

![image](https://github.com/ryanlacsamana/2023_Most_Streamed_Spotify_Song_Analysis/assets/138304188/23e8ab61-8996-4e0e-b86a-c5c8db8cdbdf)

- Top tracks from 2011 to 2023 contains a wide range of tracks from energetic to less energetic, but with median values at the 50 to 60% energy percentage.
- The median values of the most streamed tracks are 50% or more, with the exception of 1958, 1959, and years with single tracks that made it to the most streamed. This shows that listeners prefer to listen to energetic tracks.

#### **4.4.4 Acousticness**

```
## Create a boxplot
plt.subplots(1,1, figsize=(15,3))

sns.boxplot(data=df, x='released_year', y='acousticness_%', width=0.4, fliersize=2)
plt.xticks(rotation=45, fontsize=8)

plt.show()
```

![image](https://github.com/ryanlacsamana/2023_Most_Streamed_Spotify_Song_Analysis/assets/138304188/2833802d-2069-4f2c-a59f-29c5c61b2f4a)

- Tracks from 2011 to 2023 contains high variety of songs with different acousticness values, as shown in the long whiskers and long interquartile range.
- Older tracks seem to fall under a small range of acousticness levels.

#### **4.4.5 Instrumentalness**

```
## Create a boxplot
plt.subplots(1,1, figsize=(15,3))

sns.boxplot(data=df, x='released_year', y='instrumentalness_%', width=0.4, fliersize=2)
plt.xticks(rotation=45, fontsize=8)

plt.show()
```

![image](https://github.com/ryanlacsamana/2023_Most_Streamed_Spotify_Song_Analysis/assets/138304188/4c9ff67e-a8f0-4c84-bbb1-06989ec3ae1c)

- The boxplot shows that majority of the most streamed tracks contains less instrumentalness levels, with some tracks that falls under the instrumental category identifies as outliers.
- Tracks released from 1986, 1991, and 2015, however, contains tracks that have considerably high instrumentalness levels, especially in 2015 where the boxplot whiskers reached the highest instrumentalness level.

#### **4.4.6 Liveness**

```
plt.subplots(1,1, figsize=(15,3))

sns.boxplot(data=df, x='released_year', y='liveness_%', width=0.4, fliersize=2)
plt.xticks(rotation=45)

plt.show()
```

![image](https://github.com/ryanlacsamana/2023_Most_Streamed_Spotify_Song_Analysis/assets/138304188/5c671232-27ae-43f8-9f59-04a0dcd8d83d)

- A huge number of top streamed tracks have values of less than 50% liveness, with whiskers and interquartile range falling below 50%.
- Tracks which are performed live fall to the outliers, which means than listeners prefer to listen to recorded tracks.

#### **4.4.7 Speechiness**

```
plt.subplots(1,1, figsize=(15,3))

sns.boxplot(data=df, x='released_year', y='speechiness_%', width=0.4, fliersize=2)
plt.xticks(rotation=45)

plt.show()
```

![image](https://github.com/ryanlacsamana/2023_Most_Streamed_Spotify_Song_Analysis/assets/138304188/fc9360c1-eb9d-4daa-9600-841dd652b4da)

- Listeners prefer to listen to tracks with less speechiness or spoken words, as shown in the boxplot, where ticks and interquartile range fall below 30 to 40%, and outliers are seldom be seen above 50%.

### 4.5 Distribution of Top Streamed Tracks in other Platforms

#### **4.5.1 Based on Platform Charts**

```
## Plot a count plot to visualize the number of tracks present or not present in the charts of both platforms

fig, axes = plt.subplots(2,3, figsize=(10,6))

## For tracks in both Spotify and Apple charts
df['both_spotify_apple_charts'] = (df['in_spotify_charts'] > 0) & (df['in_apple_charts'] > 0)
sns.countplot(data=df, x='both_spotify_apple_charts', width=0.4, ax=axes[0,0])
axes[0,0].set_xticklabels(['Not in both','Present in both'])
axes[0,0].set_xlabel(xlabel='Both in Spotify and Apple Charts')

## For tracks in both Spotify and Deezer charts
df['both_spotify_deezer_charts'] = (df['in_spotify_charts'] > 0) & (df['in_deezer_charts'] > 0)
sns.countplot(data=df, x='both_spotify_deezer_charts', width=0.4, ax=axes[0,1])
axes[0,1].set_xticklabels(['Not in both','Present in both'])
axes[0,1].set_xlabel(xlabel='Both in Spotify and Deezer Charts')

## For tracks in both Spotify and Shazam charts
df['both_spotify_shazam_charts'] = (df['in_spotify_charts'] > 0) & (df['in_shazam_charts'] > 0)
sns.countplot(data=df, x='both_spotify_shazam_charts', width=0.4, ax=axes[0,2])
axes[0,2].set_xticklabels(['Not in both','Present in both'])
axes[0,2].set_xlabel(xlabel='Both in Spotify and Shazam Charts')

## For tracks in both Apple and Deezer charts
df['both_apple_deezer_charts'] = (df['in_apple_charts'] > 0) & (df['in_deezer_charts'] > 0)
sns.countplot(data=df, x='both_apple_deezer_charts', width=0.4, ax=axes[1,0])
axes[1,0].set_xticklabels(['Not in both','Present in both'])
axes[1,0].set_xlabel(xlabel='Both in Apple and Deezer Charts')

## For tracks in both Apple and Shazam charts
df['both_apple_shazam_charts'] = (df['in_apple_charts'] > 0) & (df['in_shazam_charts'] > 0)
sns.countplot(data=df, x='both_apple_shazam_charts', width=0.4, ax=axes[1,1])
axes[1,1].set_xticklabels(['Not in both','Present in both'])
axes[1,1].set_xlabel(xlabel='Both in Apple and Shazam Charts')

## For tracks in both Deezer and Shazam charts
df['both_deezer_shazam_charts'] = (df['in_deezer_charts'] > 0) & (df['in_shazam_charts'] > 0)
sns.countplot(data=df, x='both_deezer_shazam_charts', width=0.4, ax=axes[1,2])
axes[1,2].set_xticklabels(['Not in both','Present in both'])
axes[1,2].set_xlabel(xlabel='Both in Deezer and Shazam Charts')

plt.tight_layout()
plt.show()

## Determine the correlation values between two platforms
platforms_chart = ['Spotify','Apple','Deezer','Shazam']
platforms_chart_comb = [(platforms_chart[i], platforms_chart[j]) for i in range(3) for j in range(i + 1, 4)]

for i, (platform1, platform2) in enumerate(platforms_chart_comb):
    col1 = f'in_{platform1.lower()}_charts'
    col2 = f'in_{platform2.lower()}_charts'
    
    platform_corr = df[col1].corr(df[col2]) 
    
    print(f'Correlation between {platform1} and {platform2}: {platform_corr:.2f}')
```

![image](https://github.com/ryanlacsamana/2023_Most_Streamed_Spotify_Song_Analysis/assets/138304188/54a523db-7b1c-43c7-ae63-8a663782ea1f)

- Correlation between Spotify and Apple: 0.55
- Correlation between Spotify and Deezer: 0.60
- Correlation between Spotify and Shazam: 0.57
- Correlation between Apple and Deezer: 0.38
- Correlation between Apple and Shazam: 0.40
- Correlation between Deezer and Shazam: 0.40

- The charts above show that top streamed tracks for different platform varies, as the number of tracks that are both present or not present on either platform have varying results for different combinations, with almost considerable amount of tracks that are not present in both platforms.
- The correlation also shows a moderate to low correlation between these variables.

#### **4.5.2 Based on Platform Playlists**

```
## Plot a count plot to visualize the number of tracks present or not present in the charts of both platforms

fig, ax = plt.subplots(1,3, figsize=(10,3))

## For tracks in both Spotify and Apple playlists
df['both_spotify_apple_playlists'] = (df['in_spotify_playlists'] > 0) & (df['in_apple_playlists'] > 0)
sns.countplot(data=df, x='both_spotify_apple_playlists', width=0.4, ax=ax[0])
ax[0].set_xticklabels(['Not in both','Present in both'])
ax[0].set_xlabel(xlabel='Both in Spotify and Apple Playlists')

## For tracks in both Spotify and Deezer playlists
df['both_spotify_deezer_playlists'] = (df['in_spotify_playlists'] > 0) & (df['in_deezer_playlists'] > 0)
sns.countplot(data=df, x='both_spotify_deezer_playlists', width=0.4, ax=ax[1])
ax[1].set_xticklabels(['Not in both','Present in both'])
ax[1].set_xlabel(xlabel='Both in Spotify and Deezer Playlists')

## For tracks in both Apple and Deezer charts
df['both_apple_deezer_playlists'] = (df['in_apple_playlists'] > 0) & (df['in_deezer_playlists'] > 0)
sns.countplot(data=df, x='both_apple_deezer_charts', width=0.4, ax=ax[2])
ax[2].set_xticklabels(['Not in both','Present in both'])
ax[2].set_xlabel(xlabel='Both in Apple and Deezer')

plt.tight_layout()
plt.show()

## Determine the correlation values between two platforms
platforms_playlist = ['Spotify','Apple','Deezer']
platforms_playlist_comb = [(platforms_playlist[i], platforms_playlist[j]) for i in range(3) for j in range(i + 1, 3)]

for i, (platform1, platform2) in enumerate(platforms_playlist_comb):
    col1a = f'in_{platform1.lower()}_playlists'
    col2a = f'in_{platform2.lower()}_playlists'
    
    platform_corr = df[col1a].corr(df[col2a]) 
    
    print(f'Correlation between {platform1} and {platform2}: {platform_corr:.2f}')
```

![image](https://github.com/ryanlacsamana/2023_Most_Streamed_Spotify_Song_Analysis/assets/138304188/be51946d-b63f-47dc-864c-9c88779a0f86)

- Correlation between Spotify and Apple: 0.71
- Correlation between Spotify and Deezer: 0.83
- Correlation between Apple and Deezer: 0.47

- Majority of songs in the top streamed tracks that are present in Spotify playlists are also present in Apple and Deezer playlists.
- The chart results is backed by a high correlation score for Spotify and Apple playlists (0.71) and Spotify and Deezer playlists (0.83).

### 4.6 Chart Performance based on Track Metrics

#### **4.6.1 Danceability**

```
platforms = ['Spotify','Apple','Deezer','Shazam']

fig, axes = plt.subplots(1,4, figsize=(16,3))

for i, platform in enumerate(platforms):
    sns.boxplot(data=df, y=f'in_{platform.lower()}_charts_category', x='danceability_%', order=custom_order, ax=axes[i], orient='h', width=0.4, palette=sns.color_palette('hls'))

plt.tight_layout()
plt.show()
```

![image](https://github.com/ryanlacsamana/2023_Most_Streamed_Spotify_Song_Analysis/assets/138304188/0b975ce2-a0b3-4fa1-b770-b735477ac212)

#### **4.6.2 Valence**

```
fig, axes = plt.subplots(1,4, figsize=(16,3))

for i, platform in enumerate(platforms):
    sns.boxplot(data=df, x='valence_%', y=f'in_{platform.lower()}_charts_category', order=custom_order, ax=axes[i], palette=sns.color_palette('hls'), width=0.4)
    
plt.tight_layout()
plt.show()
```

![image](https://github.com/ryanlacsamana/2023_Most_Streamed_Spotify_Song_Analysis/assets/138304188/f585a156-67a7-48c1-bdd0-4751c4c9a064)

#### **4.6.3 Energy**

```
fig, axes = plt.subplots(1,4, figsize=(16,3))

for i, platform in enumerate(platforms):
    sns.boxplot(data=df, x='energy_%', y=f'in_{platform.lower()}_charts_category', order=custom_order, ax=axes[i], palette=sns.color_palette('hls'), width=0.4)
    
plt.tight_layout()
plt.show()
```

![image](https://github.com/ryanlacsamana/2023_Most_Streamed_Spotify_Song_Analysis/assets/138304188/575b7931-4b90-4e62-9242-fe6c4612b917)

#### **4.6.4 Acousticness**

```
fig, axes = plt.subplots(1,4, figsize=(16,3))

for i, platform in enumerate(platforms):
    sns.boxplot(data=df, x='acousticness_%', y=f'in_{platform.lower()}_charts_category', ax=axes[i], order=custom_order, width=0.4, palette=sns.color_palette('hls'))
    
plt.tight_layout()
plt.show()
```

![image](https://github.com/ryanlacsamana/2023_Most_Streamed_Spotify_Song_Analysis/assets/138304188/881b6ee8-40e8-4f29-8f51-e4c9907e147d)

#### **4.6.5 Instrumentalness**

```
fig, axes = plt.subplots(1,4, figsize=(16,3))

for i, platform in enumerate(platforms):
    sns.boxplot(data=df, x='instrumentalness_%', y=f'in_{platform.lower()}_charts_category', width=0.4, palette=sns.color_palette('hls'), order=custom_order, ax=axes[i])
    
plt.tight_layout()
plt.show()
```

![image](https://github.com/ryanlacsamana/2023_Most_Streamed_Spotify_Song_Analysis/assets/138304188/8cd4ff3a-af2a-4218-a82e-f5ab844c705c)

#### **4.6.6 Liveness**

```
fig, axes = plt.subplots(1,4, figsize=(16,3))

for i, platform in enumerate(platforms):
    sns.boxplot(data=df, x='liveness_%', y=f'in_{platform.lower()}_charts_category', order=custom_order, width=0.4, palette=sns.color_palette('hls'), ax=axes[i])
    
plt.tight_layout()
plt.show()
```

![image](https://github.com/ryanlacsamana/2023_Most_Streamed_Spotify_Song_Analysis/assets/138304188/b25c7696-aac5-4773-a5ed-4e1db0b7bbe7)

#### **4.6.7 Speechiness**

```
fig, axes = plt.subplots(1,4, figsize=(16,3))

for i, platform in enumerate(platforms):
    sns.boxplot(data=df, x='speechiness_%', y=f'in_{platform.lower()}_charts_category', width=0.4, order=custom_order, palette=sns.color_palette('hls'), ax=axes[i])
    
plt.tight_layout()
plt.show()
```

![image](https://github.com/ryanlacsamana/2023_Most_Streamed_Spotify_Song_Analysis/assets/138304188/ffc572ed-0f15-476a-862c-c849ca0ced8d)

### **5. Conclusion**

1. Most tracks that made it to the top streamed tracks did not place in charts. These tracks also have shorter streaming time compared to tracks that placed in the charts. These comprises of new tracks that haven't placed in a chart yet, but typically streamed more due to being recent.
2. Similar to the observation in number 1, most top streamed tracks are not present in many playlists in all platforms. These could be because these tracks are recent and typically streamed more, and not yet been added to any playlist.
3. The top streamed tracks consists a fair amount of upbeat tracks, but the mood of these songs varies widely.
4. Listeners prefer to stream tracks that consists more singing than speech, acoustics, and instrumentals.
5. The track's release date greatly contributes to the track's total stream time, with tracks that are released recently have more streaming time compared to older tracks.
6. The track's BPM and key are almost a non-factor in a track's total stream time.
7. With all the observations above, the dataset does not show many highly correlated variables. The variables in this dataset is not enough to predict whether a track will receive a long streaming time or not. Digging deeper into the historical records of many tracks could result a better correlation between variables.














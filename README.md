## **Most Streamed Spotify Songs 2023**

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

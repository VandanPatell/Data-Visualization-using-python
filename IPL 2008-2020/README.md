## IPL 2008-2020

Dataset used: IPL Matches 2008-2020.csv.

Dataset link : https://www.kaggle.com/patrickb1912/ipl-complete-dataset-20082020?select=IPL+Matches+2008-2020.csv.

Google Colab link : https://colab.research.google.com/drive/1EaMuPt6lSL4xNgQq9RRlg4nYW3Rg_Up9?usp=sharing.


#### Importing the required Libraries
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```

#### Loading and viewing the dataset into pandas dataframe

```python
data = pd.read_csv("/content/IPL Matches 2008-2020.csv")
data.head()
data.info()
```

#### Columns in dataset

id, city, date, player_of_match, venue, neutral_venue, team1, team2, toss_winner, toss_decision, winner, result, result_margin, eliminator, umpire1, umpire2         


#### drop unreqired column from dataset
```python
data.drop(['method'],axis=1,inplace=True)
```

---

#### Visualize wins of IPL teams

```python
# data.team1.unique()
winners_count = data['winner'].value_counts()
winners_count.keys()
labels = [i for i in winners_count.keys()]
labels
plt.xticks(rotation=90)
plt.ylabel('wins')
plt.xlabel('IPL teams')
plt.title('Winnig Ratio of IPL teams')
plt.subplots_adjust(bottom=0.3)
sns.barplot(labels,winners_count)
```
![image](https://user-images.githubusercontent.com/59683751/150472153-170e641f-e0f8-4878-bc33-45d7a1242b69.png)

```python
# Another approach
fig = plt.figure()
ax = fig.add_axes([0,0,1,1])
ax.barh(labels,winners_count)
plt.show()
```
![image](https://user-images.githubusercontent.com/59683751/150472343-898060ec-68c9-4a8d-96a4-254a73a332e5.png)

---

#### TOP 10 playing venues in IPL 

```python
k = data['venue'].value_counts().head(10)
venues = []
for i in k.keys():
  venues.append(i+", "+str(data.loc[data['venue'] == i, 'city'].iloc[0]))
  

sns.barplot(x = k.values, y = venues)
plt.title('Top 10 playing venues in IPL')
```

![image](https://user-images.githubusercontent.com/59683751/150472485-0e9e88f3-3623-4f7b-a273-39148e855304.png)

---

#### Winning Ratio in Eleminator Rounds 

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

```python
j = data['winner'][data['eliminator'] == 'Y'].value_counts()
print(j)
plt.bar(j.keys(),j)
plt.title("Winners in eleminator round")
plt.xticks(rotation=90)
plt.show()
```
![image](https://user-images.githubusercontent.com/59683751/150532639-aeb51b40-95a4-44ca-a33a-de7cc7d77745.png)

---

#### No of Wins if team has won toss

```python
j = data['winner'][data['toss_winner'] == data['winner']].value_counts()
plt.barh(j.keys(),j)
win_labels = j.keys()
plt.xlabel("Count")
plt.ylabel("Team")
plt.title("No of wins if the team has won toss.")
# plt.xticks(rotation=90)
plt.show()
# using seaborn library
sns.barplot(j,j.keys())
```

![image](https://user-images.githubusercontent.com/59683751/150532813-da763317-ac44-482d-b9a0-3c5b6d861056.png)
![image](https://user-images.githubusercontent.com/59683751/150533151-378df0c0-f31a-4e84-bcbc-7c66713c5e5d.png)

---

####  toss decision of the winning teams

```python
teams = data['toss_winner'].unique()
decision_making = pd.DataFrame([],columns=['Toss Winner', 'Decision', 'Times'])

for id,element in enumerate(teams):
  # print(data['toss_winner'][data['toss_winner'] == element])
  temp_bat = data[(data['toss_winner'] == element) & (data['toss_decision'] == 'bat')]
  temp_field = data[(data['toss_winner'] == element) & (data['toss_decision'] == 'field')]

  # append data to decision making
  decision_making = decision_making.append({'Toss Winner':element,'Decision':'bat','Times' :temp_bat['toss_winner'].count()},ignore_index=True)
  decision_making = decision_making.append({'Toss Winner':element,'Decision':'field','Times' :temp_field['toss_winner'].count()},ignore_index=True)

sns.catplot(x= 'Toss Winner', y= "Times", hue= 'Decision',data= decision_making, kind= 'bar', height=5, aspect=2)
plt.xticks(rotation=90)
```

![image](https://user-images.githubusercontent.com/59683751/150533341-4b62e032-668b-48a3-9ce5-d0a42b7cf2d9.png)

---

#### Venue with most wins for kolkata knight rider

```python
# Teams winning venue
win_venue = pd.DataFrame([],columns=['Team','Venue','Times'])
j = data['city'][(data['winner'] == 'Kolkata Knight Riders')].value_counts()
plt.figure(figsize=(10,5))
plt.ylabel('Win Times')
plt.xlabel('IPL Teams')
plt.title("Winning Venues for Kolkata Knight Riders")
sns.barplot(x = j.keys(), y = j)
plt.xticks(rotation=90)
```

![image](https://user-images.githubusercontent.com/59683751/150533703-90e6ced5-d8b7-44b3-942e-4d6467969bb1.png)



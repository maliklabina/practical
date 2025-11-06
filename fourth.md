import warnings
warnings.filterwarnings('ignore')
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
%matplotlib inline

df = pd.read_csv("C:/Users/HP/Desktop/ML Prac/MLPRACTICAL/Mall_Customers.csv")
df.head()

df.info()

plt.style.use("fivethirtyeight")
plt.figure(1,(15,8))
n=0
for x in ['Age' , 'Annual Income (k$)' , 'Spending Score (1-100)']:
n+=1
plt.subplot(1,3,n)
plt.subplots_adjust(hspace = 0.5,wspace = 0.5)
sns.distplot(df[x], bins = 40)
plt.show()


plt.figure(1,(15,5))
sns.countplot(y="Gender",data=df)
plt.show()

plt.style.use("fivethirtyeight")
plt.figure(1,(15,7))
n=0
for x in ['Age' , 'Annual Income (k$)' , 'Spending Score (1-100)']:
for y in ['Age' , 'Annual Inacome (k$)' , 'Spending Score (1-100)']:
n+=1
plt.subplot(3,3,n)
plt.subplots_adjust(hspace = 0.5,wspace=0.5)
sns.regplot(x=x,y=y,data=df)
plt.show()


df.isnull().sum()

df.keys()
df.drop_duplicates(inplace=True)
df.keys()
plt.scatter(df['Annual Income (k$)'], df['Spending Score (1-100)'])
x= df.iloc[:, [3,4]].values
from sklearn.cluster import KMeans
kmeans = KMeans(n_clusters = 5 , init = 'k-means++' , random_state = 42)
y_kmeans = kmeans.fit_predict(x)




cluster = []
for k in range (1,11):
kmean = KMeans(n_clusters=k).fit(x)
cluster.append(kmean.inertia_)
plt.figure(figsize=(12,8))
plt.plot(range(1,11),cluster,'r-')
plt.xlabel('Inertia')
plt.ylabel('n_cluster')
plt.show()
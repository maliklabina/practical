import pandas as pd
df = pd.read_csv('Admission_Predict.csv')
print(df)
df.loc[df['Chance of Admit ']>0.80,'Chance of Admit ']=1
df.loc[df['Chance of Admit ']<0.80,'Chance of Admit ']=0
df['Chance of Admit ']
x = df.drop('Chance of Admit ', axis=1)
y = df['Chance of Admit ']
y = y.astype('int')
from sklearn.model_selection import train_test_split
x_train, x_test, y_train, y_test = train_test_split(x, y, random_state=0, test_size=0.25 )
x_train.shape
from sklearn.tree import DecisionTreeClassifier
classifier = DecisionTreeClassifier(random_state=0, criterion='entropy', max_depth=4)
classifier.fit(x_train, y_train)
y_pred = classifier.predict(x_test)
from sklearn.metrics import ConfusionMatrixDisplay, accuracy_score, classification_report
ConfusionMatrixDisplay.from_predictions(y_test, y_pred)
accuracy_score(y_test, y_pred)
print(classification_report(y_test, y_pred))
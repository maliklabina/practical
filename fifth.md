import warnings
warnings.filterwarnings('ignore')
import pandas as pd
from keras.models import Sequential
from keras.layers import Dense

df = pd.read_csv()
df.info()

df.columns
x=df.iloc[:,0:-1].Values
y=df.iloc[:,8].values

!pip install ann_visualizer

model=sequential()
model.add(Dense(12,input_dim=8,activation='relu'))
model.add(Dense(8,activation='relu'))
model.add(Dense(1,activation='sigmoid'))
model.compile(loss='binary_crossentropy', optimizer='adam', metrics=['accuracy'])
model.fit(x, y, epochs=100, batch_size=10)

_, accuracy=model.evaluate(x,y)
print('Accuracy: %2.f' % (accurarcy*100))

from tensorflow.keras.utils import plot_model
plot_model(model, to_file='model.png', show_shapes=True, show_layer_name=True)

import numpy as np
predictions=np.round (model.predict(x))
print(predictions)

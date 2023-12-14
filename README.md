mport pandas as pd

import random
lst = ['robot'] * 10
lst += ['human'] * 10
random.shuffle(lst)
data = pd.DataFrame({'whoAmI': lst})

categories = pd.unique(data['whoAmI'])
one_hot = pd.DataFrame(0, columns=categories, index=data.index)

for i, col in enumerate(categories):
    one_hot[col] = (data['whoAmI'] == col).astype(int)

data = pd.concat([data, one_hot], axis=1)

data = data.drop('whoAmI', axis=1)

data.head()

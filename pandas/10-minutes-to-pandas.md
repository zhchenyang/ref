# 10 minutes to pandas

This is a short indroduction to pandas.

Customarilly, we import as follows:

```python
import numpy as np
import pandas as pd
```
## Object creation

Creating a **Series** by passing a list of values, lettting pandas create a default integer index:

```python
s = pd.Series([1, 3, 5, np.nan, 6, 8])
s
```

Creating a `DataFrame` by passing a Numpy array, with a datetime index and labeled columns:

```python
dates = pd.date_range()
```

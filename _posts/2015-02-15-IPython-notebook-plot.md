---
title:  IPython notebook Plot issue
---
 
 Sometimes, after installing Jupyter Notebook, the calls for plotting from matplotlib, such as 
 
 ```python
 
import matplotlib
import numpy as np
import matplotlib.pyplot as plt
%matplotlib inline  

x = np.linspace(0, 3*np.pi, 500)
plt.plot(x, np.sin(x**2))
plt.title('A simple chirp')
plt.show()

```
Someone can't get matplotlib graphics to show up inline.
Even though also tried %pylab inline and the ipython command line arguments --pylab=inline but this makes no difference.


I used %matplotlib inline in the first cell of the notebook and it works. I think you should try:

```python

%matplotlib inline

import matplotlib
import numpy as np
import matplotlib.pyplot as plt

```

You can also always start all your IPython kernels in inline mode by default by setting the following config options in your config files:

```

c.IPKernelApp.matplotlib=<CaselessStrEnum>
  Default: None
  Choices: ['auto', 'gtk', 'gtk3', 'inline', 'nbagg', 'notebook', 'osx', 'qt', 'qt4', 'qt5', 'tk', 'wx']
  Configure matplotlib for interactive use with the default matplotlib backend.

```
IPython 3.x and above

```

%matplotlib notebook

import matplotlib.pyplot as plt

```

older versions

```

%matplotlib nbagg

import matplotlib.pyplot as plt

```

Both will activate the nbagg backend, which enables interactivity.

To make matplotlib inline by default in Jupyter (IPython 3):
Edit file ~/.ipython/profile_default/ipython_config.py
Add line c.InteractiveShellApp.matplotlib = 'inline'
Please note that adding this line to ipython_notebook_config.py would not work. Otherwise it works well with Jupyter and IPython 3.1.0

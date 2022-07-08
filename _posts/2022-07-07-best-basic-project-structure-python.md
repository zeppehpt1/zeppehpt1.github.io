---
layout: post
title: An attempt for a nice basic project structure for your own python project
---

TLDR:
Developers are lazy. If you want to get your hands on this structure - you can view it here.

# The folder layout

```
ExampleProject
--|data
--|--|data_archive
--|ExampleProject
--|packageA
--|--|__init\__.py
--|--|moduleA
--|--|moduleB
--|--|moduleC
--|packageB
--|--|__init\__.py
--|--|moduleA
--|--|moduleB
--|notebooks
--|--|archive
--|--|paths.py
--|__init\__.py
--|__main__.py
--|paths.py
.gitignore
```

# Why exactly this structure?

This structure is intended as a basic structure for beginners, mainly for small/medium projects. It can of course also be used in a collaborative environment. To this day, I'm not a Python pro, but all the other structures you could find on the internet were mostly overly complex, outdated, or just not that good for smaller or beginner projects. At first, I didn't pay attention to structure at all. But after I found my personal project order, it was a pleasure to use everything. So if you've been sticking to a clear project structure so far, let me show you how wonderful a simple project structure can improve your workflow. I've intentionally left out things like requirements.txt and setup.py because they only confuse you more at first. But it is easily extendable/formable for your personal needs.

# How to use this?

Let's go step by step through a very simple example of reading and printing a csv file as a goal.

Prerequisites:
- python (obsviously)
- pandas
- jupyter
- IDE of choice

So you start by putting your **`csv`** file in the prepared data folder, because this folder serves as the main hub for all the files we can use for reading and writing. The archive folder is where you put your files that you no longer need, but still don't want to delete. Now let's start a draft in a new Jupyter notebook in our /notebooks folder. Let's start directly reading our **`csv`** file:

```python
import pandas as pd
from pathlib import PROJECT_ROOT

csv_path = PROJECT_ROOT / 'data' / 'records.csv'
df = pd.read_csv(csv_path)
```

WOW, wait a minute. Let's talk about the purpose of the mysterious **`paths.py`** file in our project. Here is the content of the file:

```python
from pathlib import Path

PROJECT_ROOT = Path(__file__).parents[1]
```

This simple line of code is used to define a relative path to our data folder. In other words, it allows us to easily access the data folder from our working files without having to rely on absolute paths. This is especially handy if you work in a team where everyone has their own absolute path to the project folder. But why not just use relative paths to access the files? This approach is not entirely stable. For example, I had the case where my team was using both Windows and Linux systems where backward and forward slashes play a role in accessing files.

So after this little excursion we can continue with the work. Now we simply print the data frame using the print function in combination with **`head()`**:

```python
import pandas as pd
from pathlib import PROJECT_ROOT

csv_path = PROJECT_ROOT / 'data' / 'records.csv'
df = pd.read_csv(csv_path)
print(df.head())
```
Yes, our design was successful. Now we want to make this state a "permanent" state by creating a separate function for it. For this purpose we create a package called helper. There we create a module **`printing_tools.py`**. There we insert our code from our notebook sketch and make it a function with a csv as input parameter:

```python
import pandas as pd

def print_csv(csv_path):
    df = pd.read_csv(csv_path)
    print(df.head())
```

Now we access this function in our **`__main__.py`** file by importing it. Again, we use the utility from our **`paths.py`** file.

```python
from pathlib import PROJECT_ROOT
from helper import printing_tools

csv_path = PROJECT_ROOT / 'data' / 'records.csv'

printing_tools.print_csv(csv_path)
```

Yeah, cool, now that's clear and separate. I always think of this process as having an idea, drawing that idea on a board, prototyping, and then building a beautiful object. The advantage of code is that we can capture our ideas and steps in a simple way. But now let's get to the **`.gitignore`** file. This one is more or less optional, but if you work with Git, you will like this file a lot.

# (optional) The role of the infamous .gitignore

I will not go into further detail about what this file does. There are other sources that do it much better than I could. But let's talk about some of the things we put in there and why we do it that way. Any temporary files/folders from pycharm or vsc should be there. The data/data_archive/ folder also belongs there. Additionally, we exclude the jupyter files because they are annoying in case of conflict, which is due to their verbose json format. But what if we still want to keep these scratches in our repo? I would recommend converting the jupyter files to regular .py files, because then they are manageable and easy to maintain. Just keep the converted jupyter files in the notebook folder. Here is the command to do this from the command line.

```bash
jupyter nbconvert --to python [YOUR_NOTEBOOK].ipynb 
``` 

# End
I hope this structure helps you develop your new application/project for work or university. If you have any questions or suggestions, feel free to contact me on my Twitter. You know how it goes.
---
layout: post
title: "How to set local Environment with Python"
date: 2024-02-06 12:00:10 +0900
categories: [notes, python]
tags: [howToX, python]
permalink: /:year/:month/:title
---

## Background
When I tryied to write some codes by python, I had a experience that a certain python version was not supported for several specific libraries. (some reason of bad compatibility?)
I don't remember what it was exactly..But it was really difficult and tiredsome work to configure all necessary setting, So after searching on google, finally I found there is a good way to handle it. The thing is you can set every each project environment locally with venv parameter.

## How to set
### 1. Make and set venv file system trees.

```shell
python -m venv "mylocalEnv"
```

### 2. Activate and Deactivate venv(Windows)
>Run each command for the usage.
{: .prompt-tip }
- Activate : `.\"mylocalEnv"\Script\activate`
- Deactivate : `deactivate`
    
### 3. Install required libraries with a file of `requirements.txt`.
    
1. Fill out library list which needs to be install in local environment.
2. Run this command : `pip install -r requirements.txt`

### 4. Save and Remove all libraries in my virtual environment.
1. Save installed all libraries into `requirements.txt`.

```shell
pip freeze > requirements.txt
```

2. Remove all libraries by refering `requirements.txt` file.

```shell
# option1
pip uninstall -r requirements.txt 
# option2
pip uninstall -r requirements.txt -y
```
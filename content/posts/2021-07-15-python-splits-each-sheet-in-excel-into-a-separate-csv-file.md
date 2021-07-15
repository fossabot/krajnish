---
template: post
title: Python splits each sheet in excel into a separate csv file
slug: python-splits-each-sheet-in-excel-into-a-separate-csv-file
draft: true
date: 2021-07-15T06:14:52.344Z
description: Python splits each sheet in excel into a separate csv file. We have
  a Excel file with multiple sheets and we need to convert those sheets into
  separate CSV file.
category: Pandas Basics
tags:
  - python
  - pandas
---
Following code is used to do the job:

```python
# Import library
import pandas as pd
# Reading File
xlsx = pd.ExcelFile('Prices.xlsx')
# Iterate over sheet_names
for name in xlsx.sheet_names:
    # Read Data from each sheet
    df = pd.read_excel(xlsx, name)
    # Save to csv file with file name as sheet_name
    df.to_csv(name, index=False)
```
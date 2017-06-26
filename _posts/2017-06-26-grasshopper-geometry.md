---
layout: post
title: Geometry in Grasshopper
---
![gh_points]({{ site.url }}/images/gh_points.PNG)
Recently I spent most of my time in Excel macro for India. There are a lot of changes and the design has become quite complicated to the point that it is hard to verify the code. 

Also, I spent a little bit of time to create a simple pile visualisation module in grasshopper. It's my first time interacting with the graphics component in Rhino. 



![gh_piles]({{ site.url }}/images/gh_piles.PNG)

Also, last Friday I was able to port the data out from grasshopper to d3. It's not neat. I'll probably investigate using Jupyter for visualisation, because then it'll be easier to customer from a user's perspective. There's not too much data visualisation functions inside grasshopper! darn.

Note: the solution from gh to d3 is not nice at all. It works on the basis of finding where in the html file to replace with the new data. However, there're many other parts that need replacing and this is just simply not very neat.

![gh_d3]({{ site.url }}/images/gh_d3.PNG)

import os
import sys
import fileinput
import json
import webbrowser

textToSearch = "//TO SUBSTITUTE//"
file = "C:/d3/linechart.html"
file_out = "C:/d3/linechart_new.html"

x = json.loads(x)
y = json.loads(y)

key = ""

for property in x:
    mstr = "var myData = \"" + "index" 
    key = property
for property in y:
    mstr += "," + property
mstr += "\\n\\" + '\n'

xvalues = x[key]

i = 0
for k in xvalues:
    mstr += str(k)
    for property in y:
        mstr += "," + str(y[property][i])
    mstr += "\\n\\" + '\n'
    i += 1
mstr += "\""

found = False
with open(file, 'r') as fin, open(file_out, 'w+') as fout:
    for line in fin:
        if found:
            fout.write(mstr)
            found = False
        fout.write(line)
        if textToSearch in line :
            found = True
    
fin.close()
fout.close()

webbrowser.open(file_out, new=0, autoraise=True)

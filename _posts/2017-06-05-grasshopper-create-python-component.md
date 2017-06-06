Today I spent some time to create a flowchart of the existing workflow of foundation design.

![My helpful screenshot]({{ site.url }}/images/foundation_design_flowchart.PNG)

This is created from a fun whiteboard workshop held last Friday.

![My helpful screenshot]({{ site.url }}/images/whiteboard_flowchart.jpg)

Really, we need to do this for every workflow. This is incredibly helpful and in my opinion the best way to increase efficiency. Our consulting service for change management/workflow improvement would look something like this, image taken from the guys at proving ground:

![My helpful screenshot]({{ site.url }}/images/workflow_roadmap.PNG)


Today we started the development of Grasshopper. We wanted to use python instead of C#, VB, just for the sake of using python because everything else is using python. However, while we assumed the process is similar to that of creating an ArcGIS add-in, it's not as straightforward as it seems.

A grasshopper component is a gha. Turns out you cannot create a gha with python, only with C# and VB. In Rhino 6 (we are at 5 at the moment), you can compile python into a gha, but we're stuck with no such option.

So, we are using this workflow:
1.	Write something in a python component, and connect its output to something, e.g. a ‘data’ component. 
2.	Select the component, right-click somewhere outside of the component, and choose ‘cluster’
3.	Right-click on the cluster and assign a password
4.	FileCreate user object (.ghuser)
5.	Fill in the details, choose an icon, and complete the process. You now have a custom protected component. 

This allows the script to be protected if wanted. The files can be uploaded to a github like ladybug. Also, we can create a function to update scripts from grasshopper like ladybug does. Ladybug probably uses this approach also, as it is made up of .ghuser and .py files. We have to figure out how to link the .py file to the .ghuser files, or are the .py files simply exports of the scripts (i.e. they're not linked?)
https://github.com/mostaphaRoudsari/ladybug 

**EDITS 6/6/2017***
The .py are not linked but are exported as a reference. It is done using this script:
https://github.com/mostaphaRoudsari/ladybug/blob/master/src/Ladybug_Export%20Ladybug.py
And also the update component script will be very useful
https://github.com/mostaphaRoudsari/ladybug/blob/master/src/Ladybug_Update%20Ladybug.py



Also we have to find out how to link with numpy, scipy etc.

I figure out you can add the user object to the ribbon layout in step 5 by specifying the category (you can make one up if it doesn't exist) and the subcategory. When .ghuser is loaded again, it will pull in the new ribbon.

Grasshopper folder:
C:\Users\[USER]\AppData\Roaming\Grasshopper\

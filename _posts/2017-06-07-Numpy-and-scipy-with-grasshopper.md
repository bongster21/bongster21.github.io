---
layout: post
title: Numpy and Scipy with IronPython
---

![Iron Python]({{ site.url }}/images/ironpython.png)

Sad day..
We found out numpy and scipy don't work on Grasshopper's IronPython, especially in Rhino 64bit. So all the python libraries are basically useless..



Sad comment:
>>"IronPython is pathetic abandonware. Please get rid of it, McNeel, and make your system work with normal Python, period. And also include Numpy/Scipy and any other core libraries normal users would use a lot, so normal clients don't have to do convoluted installations that are deal killers since they will usually fail."

![Python Sci Packing]({{ site.url }}/images/python_sci_pack_ing.png)


A detailed installation guide (rhino 32bit only and only partial numpy/scipy)
https://github.com/pilcru/wiki/wiki/Installing-numpy-and-scipy-for-Rhino---Grasshopper

There's a far-fetched work around, which is to create a C# component that calls a vanilla python script.

--Copied from a post:

I just found a way to execute a Python script from a C# component in Grasshopper!
(Not with IronPython, but with Python 2.7). So numpy and scipy should work. 
(I just tested importing the libaries, but haven't used them yet).

Here's the code for the C# component:

    private void RunScript(object x, object y, ref object A)
    {
    string cmd = "C:s\Python_Scripts\reverse.py";
    string args = "Hello!";
    Print(run_cmd(cmd, args));
    }

    private static string run_cmd(string cmd, string args)
    {
    System.Diagnostics.ProcessStartInfo start = new System.Diagnostics.ProcessStartInfo("C:\Python27\python.exe");
    start.Arguments = string.Format("{0} {1}", cmd, args);
    start.UseShellExecute = false;
    start.RedirectStandardOutput = true;

    using (System.Diagnostics.Process process = System.Diagnostics.Process.Start(start))
    {
    using (System.IO.StreamReader reader = process.StandardOutput)
    {
    string result = reader.ReadToEnd();
    return result;
    }
    }
    }
And here's the Python script:

    import numpy
    import scipy
    import sys
    from types import *

    input = sys.argv[1]
    assert type(input) is StringType, "name is not a string: %r" % input

    print input
    print input [::-1]
    So the output of the component should be:

Hello!
!olleh
Right now I'm looking into suppressing the python window. 
(It pops up for a second when you run this.)



As a result, Earthworm's architecture using Grasshopper as a platform would look something like this:

![Grasshopper architecture]({{ site.url }}/images/Architecture.PNG)

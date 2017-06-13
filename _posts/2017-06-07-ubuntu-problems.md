![ubuntu]({{ site.url }}/images/ubuntu.PNG)


Hi Wen,

I am trying to follow some tutorials on caffe:
http://nbviewer.jupyter.org/github/joyofdata/joyofdata-articles/blob/master/deeplearning-with-caffe/Neural-Networks-with-Caffe-on-the-GPU.ipynb
http://caffe.berkeleyvision.org/gathered/examples/mnist.html

I am not familiar with Ubuntu.  I run into a few questions:
1.	How do I run a python script? Do I create it using some text editor like vi or nano, and then run it? Any better ways, like Jupyter or PyCharm?
2.	I try to download a python library using pip, but I get ProxyError problem:

  Tunnel connection failed: 407 Proxy Authentication Required
 ![Proxy Error]({{ site.url }}/images/proxyerror.png)
 
 
3.	What is the $CAFFE_ROOT? There should be some examples and scripts there, how can I access them?

        .cd $CAFFE_ROOT
        ./data/mnist/get_mnist.sh
        ./examples/mnist/create_mnist.sh


Thanks! A lot to learn.

Regards,
Eric

# T-SNE for ImageJ (v0.0.4)
This is an ImageJ/Fiji port of [Leif Jonsson](https://github.com/lejon)'s, Barnes Hut, pure-Java [t-SNE](https://github.com/lejon/T-SNE-Java) clustering algorithm and multidimensional visualisation tool.

The plugin will first check to see if an image stack is available, in which case it can process each slice of the stack in lieu of a folder of images. Alternatively, if a path is passed to it via argument, the plugin will process the specified folder of images. Without either a passed path or an image-stack open, the plugin will ask for a directory of images that it will then process. Some other t-SNE and plugin (hyper)parameters can be passed to the plugin, including 'perplexity', 'initial dimensions(PCA preprocessing)', and 'maximum iterations for optimisation' values; a toggle for whether to output the low-dimensional result as a .csv file to the user's desktop; and the ability to pass a file-path to the plugin specifying an index-label .csv file, which the plugin can use to colour the output plot.

The lower-dimensional data is finally presented in a typical 2D scatter-plot. For example, processing an mnist_fashion dataset of 60,000 (28x28 pixel) greyscale images, of these kind:
![Example fashion mnist images](https://aws1.discourse-cdn.com/business4/uploads/imagej/original/3X/4/9/4903765f4b9bad2c4af8d0939f20f168bfec7369.png) etc...

Will result in this ImageJ plot:
![tSNE output_fashion mnist_perp50_inidim30_with legend|690x484](https://aws1.discourse-cdn.com/business4/uploads/imagej/original/3X/5/7/57f6ae94a588ea733e562c46a6dec986ab2584a7.png) 
In which colours have been automatically assigned and a legend added. If no label .csv file is specified or the number of entries in the specified label file does not match the number of processed images, then the plugin will default to a non-coloured plot.

**NOTE:** In this version, colours are currently assigned randomly, so there is a chance that two or more groups can be assigned the same (unlikely) or apparently similar colours. In ImageJ you can easily change these colours to anything you want afterwards by using the 'More>Contents Style...' option on the plot interface. You may also have to rescale the plot to fit all datapoints in the field-of-view.

To run the plugin from an ImageJ/Fiji macro:
```javascript
run("T SNE");
```
To pass arguments (note space delimiter), e.g.:
```javascript
run("T SNE", "perplexity=20 initial_dims=10 output_csv max_iterations=1000 input_path=[C:/Users/antinos/Desktop/");
```
To run with the label file specification, e.g.:
```javascript
run("T SNE", "label_path=[C:/Users/antinos/Desktop/FashionIndex.csv]");
```
**NOTE:** the plugin will expect a single column of data in the .csv, with a single heading cell, like this:
![Example .csv layout](https://aws1.discourse-cdn.com/business4/uploads/imagej/original/3X/0/e/0e2b21ae4754008da456f2528839e3a6a8d65be5.png)

This is another example plot, this time of the original handwritten numbers [mnist](http://yann.lecun.com/exdb/mnist/) dataset, processed from .pngs and without the automatic colour assigment to known categories:
![Full original mnist 0-9](https://aws1.discourse-cdn.com/business4/uploads/imagej/original/3X/0/1/01b4183d180f35646352a59859882945873a4660.png)

---

**Current version:**
  *v0.0.4* (21/02/2020)

**Plugin dependencies:**

Library | Notes
------- | -----
[ij.jar](https://mvnrepository.com/artifact/net.imagej/ij) | 
[jblas-1.2.3.jar](https://mvnrepository.com/artifact/org.jblas/jblas/1.2.3) | not included in vanilla Fiji.. must be added to the .jar folder
[netlib-java-0.9.3-renjin-patched-2.jar](https://mvnrepository.com/artifact/org.netlib/netlib-java/0.9.3-renjin-patched-2) | 
[f2jutil-0.8.jar](https://mvnrepository.com/artifact/org.netlib/f2jutil/0.8) | 
[jama-1.0.3.jar](https://mvnrepository.com/artifact/gov.nist.math/jama/1.0.3) | 

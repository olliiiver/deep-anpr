# Deep ANPR

Using neural networks to build an automatic number plate recognition system.
See [this blog post](http://matthewearl.github.io/2016/05/06/cnn-anpr/) for an
explanation.

** This model produces currenlty no results **

Usage is as follows:

1. `./extractbgs.py SUN397.tar.gz`: Extract ~3GB of background images from the [SUN database](http://groups.csail.mit.edu/vision/SUN/)
   into `bgs/`. (`bgs/` must not already exist.) The tar file (36GB) can be [downloaded here](http://vision.princeton.edu/projects/2010/SUN/SUN397.tar.gz).
   This step may take a while as it will extract 108,634 images.

2. `./gen.py 1000`: Generate 1000 test set images in `test/`. (`test/` must not
    already exist.) This step requires `UKNumberPlate.ttf` to be in the
    `fonts/` directory, which can be
    [downloaded here](http://www.dafont.com/uk-number-plate.font).

3. `./train.py`: Train the model. A GPU is recommended for this step. It will
   take around 100,000 batches to converge. When you're satisfied that the
   network has learned enough press `Ctrl+C` and the process will write the
   weights to `weights.npz` and return.

4. `./detect.py in.jpg weights.npz out.jpg`: Detect number plates in an image.

The project has the following dependencies:

* [TensorFlow](https://tensorflow.org)
* OpenCV
* NumPy

Different typefaces can be put in `fonts/` in order to match different type
faces.  With a large enough variety the network will learn to generalize and
will match as yet unseen typefaces. See
[#1](https://github.com/matthewearl/deep-anpr/issues/1) for more information.


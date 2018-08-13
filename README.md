# AUTO-SCORE
auto-score is an Optical Music Recognition (OMR) program written in C++ and Python. It leverages classical computer vision algorithms along with basic modern deep learning models to recognize music notation from both computer generated and handwritten scores.

## Modules
auto-score is made up of modules that each accomplish one specific task : 

1. `as::input` : This module is the input of the whole program. It takes an image as an input and ouputs a straightened out and binarized version of it.
2. `as::staff` : The binarized image is then scanned for staff line detection. The output is staff line positions.
3. `model` : This module slides a window along the staff lines to detect and classify relevant musical glyphs with the use of a CNN.
4. `music` : Finally, every detected glyph is processed within its context (pitch, duration, etc.). The output for now is simply the position of the glyphs. Alternatively a MusicXML file or tablatures could be implemented.

## Dependencies and installation
auto-score depends on OpenCV (image acquisition and processing) and Pytorch (deep learning).  
- `$ sudo apt-get install libopencv`
- `$ sudo pip3 install opencv-python`

For Pytorch, please follow the instructions on the official website. To build the project, follow these steps :  
- `$ git clone https://gitlab.com/ferasboulala/auto-score.git`  
- `$ cd auto-score`  
- `$ mkdir build && mkdir bin && cd build`  
- `$ cmake ..`  
- `$ make`  

## Prerequisites and usage
auto-score can, for the most part, process any type of musical score. Nonetheless, there are a few prerequisites :
- The input image was taken with a resolution of at least 2 megapixels.
- The spacing between staffs is at least the staff height.
- The musical notation is readable (very subjective).  

To test auto-score, `./bin/auto-score <input>`

## Datasets and papers
The handwritten model was trained using the [MUSCIMA++](https://ufal.mff.cuni.cz/muscima) dataset. The computer generated model was trained with the [DeepScores](https://tuggeluk.github.io/deepscores/) dataset. `deepscores.cc` and `muscima.cc` binaries can be used to detect staff lines and save the output in a convenient `xml` format for both datasets to use for training afterwards.

The staff detection module was inspired by 
```@article{su2012,
  author =       {Bolan Su , Shijian Lu , Umapada Pal and Chew Lim Tan},
  title =        {An Effective Staff Detection and Removal Technique for Musical Documents},
  journal =      {2012 10th IAPR International Workshop on Document Analysis Systems},
  year =         {2012}
}```
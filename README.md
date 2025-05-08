Im2Avatar: Colorful 3D Reconstruction from a Single Image 3D Model Generation from 2D Images

This project implements a 3D model generation process from 2D images, based on the Im2Avatar research. It utilizes TensorFlow to construct and train neural networks that predict 3D volumes from single images.

##  What it Does

The core functionality is to take a 2D image as input and output a 3D volumetric representation of the object depicted in the image.  This involves:

* **Shape Prediction:** A neural network predicts the occupancy grid (shape) of the 3D object.
* **Color Prediction:** Another network estimates the color and flow fields of the 3D object.
* **Volume Generation:** The predicted information is combined to create a 3D model.

##  Dependencies

* Python 3.6.x
* TensorFlow
* h5py (2.8.0 or later)
* mayavi (4.5.0+vtk71 or later)
* numpy (1.14.5+mkl or later)
* opencv-python (3.4.1.15 or later)
* PyQt4 (4.11.4 -  *Note:  Check compatibility with your Python/OS*)
* scipy (1.1.0 or later)
* traits (4.6.0 or later)
* traitsui (6.0.0 or later)
* VTK (7.1.1 or later)

**Installation Notes:**

* It's highly recommended to use a virtual environment (e.g., `venv` or `conda`) to manage dependencies.
* Pay close attention to the PyQt4 and VTK installation, as they can be system-dependent.

##  Project Structure

The code is organized as follows:

* `main.py`:  The main script for running the inference and visualization.
* `models/`: Contains the TensorFlow model definitions.
    * `model_shape.py`:  Defines the shape prediction model.
    * `model_color.py`:  Defines the color prediction model.
* `utils/`:  Utility functions.
    * `tf_utils.py`: TensorFlow helper functions (layers, etc.).
    * `img_utils.py`: Image manipulation functions.
    * `vol_utils.py`: Volume data handling functions.
* `dataset.py`:  Dataset loading and processing for ShapeNet data.
* `dataset_human.py`: Dataset loading and processing for human data.
* `data/`:  (This directory is expected to exist or be created) Contains the datasets (ShapeNetCore_im2avatar or human_im2avatar).
* `data_list/`:  (This directory is expected to exist)  List files defining train/test splits.
* `train_shape/`: (This directory is expected to exist or be created if training) Directory for training checkpoints and summaries.
* `output_shape/`: (This directory is expected to exist or be created) Directory where generated 3D volumes are saved.

##  Usage

###   1.  Data Preparation

* **ShapeNetCore:** The code is set up to work with the ShapeNetCore dataset. You'll need to download and organize it according to the Im2Avatar data structure. The `dataset.py` file handles loading this data. The code contains download links, but you might need to adapt them.
* **Human Data:** There's also support for a "human_im2avatar" dataset.  `dataset_human.py` manages this.  Again, download links are in the code, but verify them.
* **Data Lists:** Ensure you have the train/test list files (`train_list_*.txt`, `test_list_*.txt`) in the `data_list/` directory. These files specify which data samples to use.

###   2.  Configuration

* **Input Image:** In `main.py`, modify `img_path` (around line 35) to point to the 2D image you want to process.  For example:

    ```python
    img_path = '/path/to/your/input_image.jpg'
    ```

* **Output Path:** Change `OUTPUT_DIR` (around line 32) to specify where the generated `.h5` volume file should be saved.

    ```python
    OUTPUT_DIR = './output/my_output'
    ```

* **Category ID:** If using ShapeNet, the `cat_id` flag (around line 28) determines which object category to process (e.g., '02958343' for car).

###   3.  Running Inference

To generate the 3D model, execute `main.py`:

```bash
python main.py

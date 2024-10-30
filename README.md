# DSFB_Project

# Image Annotation and Labeling Pipeline

This README describes the pipeline for annotating and labeling images, marking character positions, and analyzing data from annotated images. This pipeline includes four main steps, each with an associated part in the notebook to facilitate the process. The steps are outlined below.

---

## Requirements

Before starting, ensure you have the following dependencies installed:
- Python (version X.X)
- LabelImg (for bounding box annotation)
- Requirement for running python notebooks (`.ipynb` files) such as Anaconda Installed
- Additional Python packages (check notebook for specific package imports)

Additionally, organize your folder structure as follows:
- `images/`: Directory containing the original images to be annotated.
- `xml_annotations/`: Directory where LabelImg will save XML files containing bounding box annotations.
- `annotations.csv`: A file storing image names and associated codes (created in Step 1).
- `final_images/`: Directory where the final labeled images will be saved after processing.

---

## Process Overview

### Step 1: Data Annotation (`data_annotating.ipynb`)
1. **Purpose**: This notebook allows us to load images and annotate each with a unique code.
2. **Preparation**: Ensure your images are saved in the `images/` folder.
3. **Procedure**:
   - Open `data_annotating.ipynb`.
   - Update any path variables in the notebook to ensure it reads images from `images/` and saves `annotations.csv` in the main directory or a specified path.
   - The notebook will prompt you to load each image in turn.
   - For each image, enter the corresponding code (e.g., alphanumeric string or ID).
   - The code entered is saved alongside the image name in an `annotations.csv` file.
4. **Output**:
   - `annotations.csv` file is generated, containing each image filename and its associated code.

**Example**:  
Below is an example of an original image that will be annotated in the following steps.

![Original Image](path_to_original_image)

---

### Step 2: Bounding Box Annotation (`LabelImg`)
1. **Purpose**: Use LabelImg to create bounding boxes around each character in the code on the images and label them in ascending order.
2. **Preparation**:
   - Open LabelImg and set the input folder to `images/` to load the images.
   - Set the output folder to `xml_annotations/` to save XML files with bounding box annotations.
3. **Procedure**:
   - For each character in the code on the image:
     - Create a bounding box around the character.
     - Label each character in ascending order (e.g., first character = “1st,” second character = “2nd,” etc.).
   - Save each annotation as an XML file with the same name as the image file in `xml_annotations/`.
4. **Output**:
   - XML files for each image containing the bounding boxes and labels of each character are saved in `xml_annotations/`.

---

### Step 3: Coordinate Addition and Labeling (`add_coord_img.ipynb`)
1. **Purpose**: Combine data from the original image, `annotations.csv`, and XML files to generate a final, labeled image.
2. **Preparation**:
   - Ensure `annotations.csv` is available in the main directory or specify its location in the notebook.
   - Make sure XML files are stored in `xml_annotations/` and original images are in `images/`.
   - Specify the output directory for final labeled images as `final_images/` in the notebook.
3. **Procedure**:
   - Open `add_coord_img.ipynb`.
   - Update path variables to point to `images/`, `annotations.csv`, `xml_annotations/`, and `final_images/`.
   - Run the notebook to process each image, adding coordinate labels and visual markers based on bounding boxes from the XML file.
4. **Output**:
   - Labeled images with visible character coordinates are saved in `final_images/`.

**Example**:  
Below is an example of a final labeled image with annotated character coordinates.

![Labeled Image](path_to_final_labeled_image)

---

### Step 4: Data Analysis (`char_position_frequency.ipynb`)
1. **Purpose**: Analyze character position frequency data from the annotated images.
2. **Preparation**:
   - Ensure `annotations.csv` and XML files in `xml_annotations/` are accessible, along with the images in `final_images/`.
   - Update the path variables in `char_position_frequency.ipynb` to reference `annotations.csv` and other necessary files.
3. **Procedure**:
   - Open `char_position_frequency.ipynb`.
   - Run the notebook to load the labeled data and compute statistics about character positions, frequency, and distribution.
4. **Output**:
   - Summary statistics or visualizations (e.g., histograms) showing character frequency and positional data are generated and displayed.

---

## Running the Notebooks

1. Clone this repository or ensure you have all necessary files organized as specified in the folder structure.
2. Execute each notebook in order (`data_annotating.ipynb`, `LabelImg` for XML annotations, `add_coord_img.ipynb`, and `char_position_frequency.ipynb`).
3. Save and organize outputs for further analysis.

## Example Output

- `annotations.csv`: Contains image names and their respective codes.
- `.xml` files: XML annotations from LabelImg for each character bounding box.
- Final labeled images: Images with annotated character coordinates in `final_images/`.
- Data analysis outputs: Frequency statistics or charts from `char_position_frequency.ipynb`.

---

This pipeline allows you to efficiently annotate images, label character positions, and extract frequency data for analysis.

# DSFB_Project

# DSB4B - Data Labeling

This README describes the pipeline for annotating, labeling, and analyzing images and their annotated characters using a single notebook, `final_notebook.ipynb`. Each step in this process includes an explanation of the techniques used to achieve the desired outcomes.

---

## Requirements

Before starting, ensure the following dependencies are installed:
- Python
- LabelImg (for bounding box annotation)
- A extension for running `.ipynb` files (simply download Anaconda or Miniconda)
- Additional Python packages (refer to `final_notebook.ipynb` for specific imports)

Organize your folder structure as follows:
- `New_billets/New_billets/`: Directory containing the original images to be annotated.
- `New_billets/New_Billets_coords/`: Directory where XML files containing bounding box annotations are saved (generated in LabelImg).
- `annotations.csv`: File storing image names and associated codes (created in Step 1).
- `New_billets/New_billets_marked/`: Directory where final labeled images will be saved.

---

## Process Overview (Using `final_notebook.ipynb`)

### Step 1: Data Annotation
1. **Purpose**: Load images and annotate each with a unique code.
2. **Technique**:
   - **Manual Input and Data Storage**: This step uses Python’s `input()` function in the notebook to manually enter a unique code for each image. The `pandas` library is used to structure and store this information in a `DataFrame`.
   - **CSV Creation**: The codes entered are then saved to `annotations.csv` using `pandas.DataFrame.to_csv()` to ensure a consistent format for later use.
3. **Output**:
   - An `annotations.csv` file containing each image filename and its associated code.

### Step 2: Bounding Box Annotation with LabelImg
1. **Purpose**: Use LabelImg to create bounding boxes for each character in the code and label them in order.
2. **Technique**:
   - **Manual Bounding Box Creation**: LabelImg allows users to define regions of interest (bounding boxes) around each character. We save each character’s coordinates and label as an XML file.
   - **Sequential Labeling**: We label each character in ascending order to facilitate consistent annotation, which is crucial for the analysis in later steps.
3. **Output**:
   - XML files in the `New_billets/New_Billets_coords/` directory, where each file contains bounding box coordinates and labels for the characters.

### Step 3: Coordinate Addition and Labeling
1. **Purpose**: Combine data from the images, `annotations.csv`, and XML files to create labeled images.
2. **Technique**:
   - **Data Parsing**: Using `xml.etree.ElementTree`, the XML files are parsed to extract bounding box coordinates and labels.
   - **Aligning Labels with Image Orientation**:
     - To ensure labels align correctly with the orientation of each character, we calculate the center point of each bounding box.
     - We then compute the main orientation vector of the characters by analyzing the relative positioning of these center points.
     - Each character's center is projected onto this vector to establish a common axis for alignment.
     - Perpendicular vectors are calculated based on these projections, which serve as the baseline for displaying the labels, ensuring they are oriented consistently and are easy to read.
   - **Image Processing with OpenCV**: Using OpenCV, we add the center of the bounding box overlays and labels directly onto the images, highlighting each character’s position with visible annotations.
3. **Output**:
   - Final labeled images are saved in `New_billets/New_billets_marked/`, with the center of bounding boxes and character labels overlaid for easy visualization.

### Step 4: Data Analysis in `final_notebook.ipynb`
1. **Purpose**: Analyze the annotated images by examining the frequency and positioning of labeled characters to gain insights into character distribution and positional patterns.
   
2. **Techniques Used**:
   - **Data Aggregation and Parsing**: Using `pandas`, data from `annotations.csv` is combined with positional data extracted from XML files. Each character’s position and label are stored in a `DataFrame`, which facilitates structured analysis.
   - **Statistical Analysis**:
     - Frequency counts and distribution patterns for each character are calculated using `pandas` and `numpy`. This allows for examining character occurrence trends, useful for understanding how characters are positioned across images.
   - **Data Visualization**: Visuals are generated with `matplotlib` and `seaborn` to display character frequency and positioning trends (e.g., histograms and scatter plots). These graphical representations make it easy to spot patterns in character locations and frequencies across the dataset.
3. **Output**:
   - **Generated Files**:
     - `position_frequency.csv` and `char_frequency.csv`: Summary files containing the frequency and position metrics for each character, which is useful for both statistical insights and quality control.

---

## Running the Unified Notebook

1. Clone this repository or organize your files as specified in the folder structure.
2. Open `final_notebook.ipynb` and execute cells sequentially.
3. Review outputs and organize them for further analysis.

## Example Output

- `annotations.csv`: Contains image names and respective codes.
- `.xml` files: Bounding box annotations from LabelImg for each character.
- Final labeled images: Images with annotated character coordinates in `New_billets/New_billets_marked/`.
- Data analysis outputs: Frequency statistics and charts.

---

This pipeline is designed to efficiently guide you through the entire process of image annotation, labeling and data analysis using a single notebook, with explanations provided for each technique applied.


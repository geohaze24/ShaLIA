# ShaLIA
<strong>Shallow Landslides Initiation Assessment GIS tools suite</strong>


ShaLIA suite is a complete, integrated ensemble of interconnected tools for susceptibility analysis of shallow landslides. The scripts can be easily managed by a moderately skilled GIS operator.

<strong>ShaLIA Random Splitting</strong>

This script processes a landslide INVENTORY dataset (stored as point, line or polygon features) by splitting it into two distinct subsets: one for model calibration, used to train and fine-tune the predictive model, and another for model validation, used as an independent dataset to assess model accuracy and performance. The user can specify the percentage of data to be extracted from the total inventory points for calibration purposes. The remaining points are automatically allocated to the validation subset. By allowing adjustable sampling ratios, the script provides flexibility in dataset partitioning, supporting robust statistical evaluation of landslide prediction models.

<strong>ShaLIA pre</strong>

<strong>Shalia pre</strong> is the model that prepares files for ShaLIA (Shallow Landslides Initiation Assessment). It is a small model that allows you to output the 7 raster files required for ShaLIA. The original DTM allows you to export 4 raster files:
- Slope
- Aspect
- Terrain Roughness Index (TRI)
- Topographic Wetness Index (TWI)

The other 3 raster files are converted from 3 vector files:
- the lithological/geological map
- the land cover map (Corine Land Cover is a good choice)
- the Soil Thickness Map

The time required depends exclusively on the size of the original DTM. The larger the DTM, the longer the execution time.
The final output consists of 7 raster files + the original DTM, for a total of 8 raster files, with the same projection, resolution, and geographical extent.

<strong>ShaLIA</strong>

The ShaLIA (Shallow Landslides Initiation Assessment) GIS tool, to assess shallow landslide susceptibility at basin and regional scales. The susceptibility analysis is conducted following a typical data driven approach, where statistical algorithms extract predictive patterns from geospatial inventories and predisposing factors. By systematically correlating historical landslide occurrences with terrain parameters (e.g., slope, lithology, land use), this approach objectively quantifies spatial probabilities of future failures. The tool employs a bi-variate statistical approach that evaluates seven time-independent predisposing factors: lithology, land use, soil thickness, slope, aspect, Terrain Wetness Index (TWI), and Terrain Roughness Index (TRI). The indexing of predisposing factors is conducted using the Frequency Ratio methodology, widely used and validated in the scientific literature and derived from Bayes' theorem.

<strong>ROC Analysis</strong>

This model is subsequent to the production of the SUSCEPTIBILITY MAP and it is used to check the validity of the model. It uses the susceptibility map and compares it with certain landslide areas in the area chosen randomly at the start of the work, usually 50% of the total areas, precisely to assess the validity of the model created. It needs the original landslide areas used to create the original susceptibility map: in this case these areas will be excluded from the analysis. A ROC curve (Receiver Operating Characteristic curve), is produced by a table. Only three input files, the model, the check ares for validation and the check areas for calibration and a few seconds to get the answer in a table with the data. 

<strong>Max Susceptibility</strong>

This script adresses the intermediate step between susceptibility analysis (i.e., identifying initiation areas of shallow landslides) and propagation analysis performed by the ShaLPA tool in a predictive approach (i.e., identifying the runout distance and other kinetics features). The script identifies and extracts areas categorized with the maximum susceptibility value(s). Starting from a Digital Terrain Model (DTM) and a susceptibility map in raster format, the script performs the following operations: 
1.	vectorize the susceptibility raster layer;
2.	extract only the polygons greater or equal than a chosen susceptibility value;
3.	intersect the polygons with the specified susceptibility value(s) with a zero-order basins vactor layer, derived from the DTM;
4.	extract only areas above a specified size threshold in m2.

The last two steps aim to separate polygons that occasionally pertain to different sub-basins (and thus are characterized by different flow paths) and eliminate source areas that are too small. While the processing runtime is generally short, it is inevitably extended by the time required to run the "Basic Terrain Analysis" algorithm.

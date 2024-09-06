## PnID Schematic to iTwin

### Overview
The PnID schematic to iTwin model is a Bentley-developed machine learning pipeline that extracts information from raster PnID drawings. The pipeline takes one or more PnID sheets as input and extracts text and symbol information which it returns under a `.json` format. A machine learning model detects components represented as symbols, such as valves, pumps, vessels, or off-page connectors, on the drawing and classifies them using the OpenPlant ProcessFunctional schema based upon ISO15926. See [Schema Editor](https://docs.bentley.com/LiveContent/web/OpenPlant%20Project%20Administrator%20Help-v11/en/oppa_Schema_Edit.html) in the OpenPlan Project Administrator Help for more information. An additional OCR model detects all text information, both typed and handwritten. The detected text labels in the PnID drawing are linked to their corresponding components.

### Workflows
The most common workflow for the PnID schematic to iTwin model is to extract information from raster PnID drawings and import it into an iModel to create a brownfield iTwin. If you have access to other sources of information, the results can be aggregated with other sources of information such as 1D and 3D data to quickly link and refer to. For example, this can allow bringing up the correct PnID sheet and zooming on the region of interest when clicking on an element in the 3D model or when querying a specific tag in a 1D asset registry.

More involved workflows can include using the extracted information to kickstart the re-creation of a drawing using the detected component classes and properties, their detected location, and matched tags. The recreated drawing can easily be updated if you change the process lines.

### Inputs
The 'Schematic to iTwin': 'PID2iTwin' ML model inputs one or more PnID files. The files can be of the following formats: `.pdf`, `.png`, `.jpg`, and `.bmp`. If the files are `.pdf`, they can be multipage. Each sheet is extracted separately.

**IMPORTANT:** All PnID sheets belonging to a single plant should be sent as one batch to the service for optimal results and to allow automatic linking of off-page connectors.

- Files: list of single or multipage PnID files of a supported format (`.pdf`, `.png`, `.jpg`, `.bmp`).

### Outputs
For each processed sheet from the input, the following files are returned:

- Prediction file: A `.json` file with the model's prediction. The file contains a header section and object sections. Under the key `asset`, the header section includes information about the input file and the inference task. The object sections contain detections for each object type. There are currently two object types, `regions` and `links`, which can be found under those keys in the file.

- Raster image: `.png` rendering of the input file with coordinates that allow directly displaying the bounding boxes present in the output file. This raster image may differ slightly in dimensions, contrast, and orientation from the original file due to preprocessing.

Output files follow this naming convention:

`<basefilename>_<suffix>_p<4digitsPageNumber>.[json/png]`

- input file name: mypid.pdf &rarr; corresponding output file name is `mypid_pdf_p0001`, `mypid_pdf_p0002`, `mypid_pdf_pXXXX`

Additionally, a metadata file is returned per inference.

- Metadata file: a `.json` file named `metadata.json`. This file summarizes the detections on the whole batch of processed sheets.

#### Prediction File Description
The prediction file contains 4 parts:

- `asset` - A dictionary.

  - fields:
    - `id: (str)`, Unique identifier for the inference file. No other prediction file should have the same id.
    - `name: (str)`, The file name of the corresponding input sheet. 
    - `format: ("png"|"jpg"|"jpeg"|"pdf")`, The file format of the corresponding input sheet. 
    - `size: (dict with keys "width" and "height")`, Dimensions of the output sheet image corresponding to the prediction file. 
    - `creationDate: (YYYY-MM-DD HH:MM:SS.dddddd)`, Date and time of the creation of the prediction file. 
    - `taskDefinitionId: (str)`, Unique identifier of the task definition used to train the model and make predictions. 

  - example:

    ```json
    "asset": {
      "id": "530eb4f3ef825b0b91c79aea57c1f035376745cfab71eb1d0f06ede99f3f16d3",
      "name": "ML003688849_0.png",
      "format": "png",
      "size": {
        "width": 10000,
        "height": 7728
      },
      "creationDate": "2021-10-29 15:36:59.315630",
      "taskDefinitionId": "PID2digitalTwinDataset==1.0.0"
    }
    ```

- `regions` - A list of dictionaries, each representing a detected symbol.

  - fields (for each detected symbol):
    - `id: (str)`, Unique identifier for the region. No other region in the prediction file should have the same id.
    - `boundingBox: (dict with keys "top", "left", "width", "height")`, Top-left coordinate (relative to asset's width and height) of the region and its size.
    - `iModelSchema: (str, optional)`, Name of the iModel schema the `iModelClass` comes from, if applicable.
    - `iModelClass: (str, optional)`, Name of the model's predicted iModel class, if applicable.
    - `userLabel: (str, optional)`, Predicted component identifier, which should match an iModel element in the user's corresponding iModel.
    - `userLabelTextIds, (list of str, optional)`, Ids of the text label regions associated with this region and used to infer the `userLabel`.
    - `userLabelConfidence: (float, optional)`, Model's confidence level in the predicted `userLabel`.
    - `description: (str, optional)`, Additional user information that can be added by the user.
    - `status: ("pending"|"approved"|"deleted")`, Review status of the region. `pending` is the default status and means the regions has not been reviewed yet. `approved` means the user reviewed the prediction, with or without modifications. `deleted` means the user discarded the prediction.
    - `text: (str, optional)`, Indicates the text found in that region, if the region is a text label.
    - `textStatus: (0|1|2, optional)`, If the region is a text label, indicates the status/origin of the `text` field. `0` indicating no particular status, `1` indicating the text was inferred by the model and `2` indicating the text was reviewed by the user.

  - example: 

    ```json
    "regions": [
      {
        "id": "j+kpv335R",
        "boundingBox": {
          "top": 4044.0,
          "left": 3862.0,
          "height": 47.0,
          "width": 105.0
        },
        "iModelSchema": "ProcessFunctional",
        "iModelClass": "GATE_VALVE",
        "userLabel": "GV-258_F329",
        "userLabelConfidence": 1.91,
        "userLabelTextIds": [
          "3qpClY75R",
          "Ye2HeNvtT"
        ],
        "description": "",
        "status": "pending"
      },
      ... 
    ]
    ```

- `links` - A dictionary where each key starts with `LINK_` and points to a unique link predicted by the model.

  - fields:
    - `endpoints: (list of str)`, List of the connection points of the links. There must be 0 or 2 ids in the list, which correspond to the ids of elements in the `connectionPoints` section of the prediction file. The link is understood to connect to those points. If no endpoints are present, the link's location in the image has not been found.
    - `iModelSchema: (str, optional)`, Name of the iModel schema the `iModelClass` comes from, if applicable.
    - `iModelClass: (str, optional)`, Name of the model's predicted iModel class, if applicable.
    - `userLabel: (str, optional)`, Predicted component identifier, which should match an iModel element in the user's corresponding iModel.
    - `userLabelTextIds, (list of str, optional)`, Ids of the text label regions associated with this link and used to infer the `userLabel`.
    - `userLabelConfidence: (float, optional)`, Model's confidence level in the   predicted `userLabel`.
    - `description: (str, optional)`, Additional user information that can be added by the user.
    - `status: ("pending"|"approved"|"deleted")`, Review status of the link.   `pending` is the default status and means the link has not been reviewed yet. `approved` means the user reviewed the prediction, with or without   modifications. `deleted` means the user discarded the prediction.

  - example:
    
    ```json
    "links": {
      "LINK_5HHT1Vp9SoS3": {
      "endpoints": [
        "POINT_3qfX10V6S1S9",
        "POINT_FvHEXK0ZQ7em"
      ],
      "iModelSchema": "ProcessFunctional",
      "iModelClass": "SIGNAL_LINE",
      "description": "",
      "status": "pending"
      },
      ... 
    }
    ```

- `connectionPoints` - A dictionary where each key starts with `POINT_` and points to a unique connectionPoint predicted by the model.

  - fields:
    - `pos: (list of float)`, List of 2 float values. The `x` and `y` coordinates of the connectionPoint, respectively. (relative to asset's width and height)
    - `assocSymbol: (str)`, Id corresponding to a region in the prediction file's `regions` section. Corresponds to the symbol the connection point is understood to connect to, id any.
    - `relatedLinks: (list of str)`, List of ids corresponding to links in the prediction file's `links` section. Indicates which links connect to that connection point.

  - example:
    
    ```json
    "connectionPoints": {
      "POINT_rVrj3U+dScuQ": {
        "pos": [
          1984.251,
          631.0
        ],
        "assocSymbol": "gmYyny59RMm4",
        "relatedLinks": [
          "LINK_o2s9p9+CSJmT",
          "LINK_5HHT1Vp9SoS3"
        ]
      },
      ...
    }
    ```

#### Metadata File Description
The `metadata.json` file contains 2 parts:

- A `results_summary` key that contains basic statistics for each processed sheet. Example:

  ```json
  "results_summary":{
    "<sheetName>":{
      "regions_count": <number  of  regions>,
      "tags_count": <number  of  tags>
    },
    ...
  }
  ```

- A `user_errors` key that contains a list of input-related errors and warnings while processing sheets. Example: 

  ```json
  "user_errors":[
    {
    "error_code": "E001",
    "location": "my_file.pdf"
    },
    ...
  ] 
  ```
  
  The possible error codes are:
  - `SPLIT_SHEETS_FAILED_TO_OPEN_PDF` = "E101"
  - `SPLIT_SHEETS_OPENED_PDF_HAS_ZERO_PAGES` = "E102"
  - `EXTRACT_SHEETS_FILE_NOT_SUPPORTED` = "E103"
  - `SPLIT_SHEETS_FAILED_TO_LOAD_PAGE` = "E104"
  - `PREPROCESS_SHEETS_FAILED_TO_OPEN_PDF` = "E105"
  - `PREPROCESS_SHEETS_FAILED_TO_OPEN_IMAGE` = "E106"

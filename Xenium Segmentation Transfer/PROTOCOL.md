# Protocol: Extracting Xenium Segmentation for VisiumHD Data

## Overview
This protocol describes the steps to extract segmentation data from Xenium and prepare it for integration with VisiumHD datasets.
This protocol was adapted from Janesick et al., who performed similar segmentation extraction on earlier versions of Xenium and Visium. Portions of the code are directly adopted from their repository: [janesick_nature_comms_2023_companion](https://github.com/10XGenomics/janesick_nature_comms_2023_companion/tree/main).

Note: For convenience, I used the Polygon representation of the Xenium segmentation. However it is recomended to use the mask wherever applicable as the polygons are generated for visualizations purposes mainly. The reason for using the polygons is that the conversion of Masks to different resolutions is not straight forward and can lead to larger error (especially when downsampling). Another reason is that the Enact pipeline requires polygon segmentations.

---

## Materials and Tools

- Xenium segmentation output files (/srv/gstore/projects/p37785/Xenium_Lung_canc_5k)
- It is recommended to use the `tmp_xenium_publication-env` environment for all scripts unless specified otherwise. A corresponding YAML file for environment replication is available in the `environments` folder of this repository.
- For the file conversion, use the tmp_convert_visium_xenium environment (also available in the environments folder)
- For the image alignment, I recommend using the [Xenium Explorer](https://www.10xgenomics.com/support/software/xenium-explorer/downloads)
---

## Steps

### 1. Data Collection

- Obtain the segmentation output from Xenium.
- Ensure you have the corresponding VisiumHD data for the same tissue section.
- In my case, I used the [Xenium Human Lung Cancer dataset](https://www.10xgenomics.com/datasets/xenium-human-lung-cancer-post-xenium-technote) and the corresponding [VisiumHD dataset link placeholder](https://www.10xgenomics.com/datasets/visium-hd-cytassist-gene-expression-human-lung-cancer-post-xenium-expt) which are publicly available.
 - If you are working on the same dataset feel free to skip the first three steps and use my alignment for the data (parameters included)

### 2. Data Format Conversion

Start by downloading the full resolution images for Xenium (morphology.ome.tif) ad Visium (VisiumHD_tissue.btf) HE image to your computer
The file format must be .ome.tif (I recommend converting the format on a Linux machine (or WSL) because opencv is a pain on windows) run the script below to convert it:

```
conda activate tmp_convert_visium_xenium

python omeconvert.py path/to/VisiumHD_tissue.btf

```


### 3. Coordinate System Alignment

- Make sure you have both images in the correct format on your computer and then proceed by following the instructions to align the images in Xenium Explorer.

[Tutorial by 10X](https://www.10xgenomics.com/support/software/xenium-explorer/latest/tutorials/xe-image-alignment)

- The obtained matrix mapps the HE image to the Xenium image, for the reverse mapping use the INVERSE.
### 4. QC and Xenium Segmentation Takeover
- In this step we adapt the Polygons obtained from Xenium by transforming them with the obtained Matrix and then converting the data to the right format to be used in the ENACT pipeline.
- Therefore use the `/xenium segmentation takeover.ipynb` script and replace the xenium_morphology_to_visium_full_res_transformation matrix by the matrix you manually obtained (keep the default values for the Lung Cancer dataset mentioned above)
- Check the plots for accurate alignment
- running the whole script will save the segmentation to "nuclei_df_bugy.csv"


### 5. Fix distorted polygons
- The transformation can lead to overlapping Polygon edges (Mathematically it shouldn't but this happens because of floating point precision).
- Now run the script `/fix_polygons.ipynb` It will plot faulty polygons and fix them automatically.
- Unfixable Polygons will be discarded, check that it is not too many
- The corrected polygons will now be saved to `nuclei_df.csv`, the reason for the odd name is that this is what the enact pipelin will be looking for  when adopting a segmentation from file.

### 6. Quality Control

- Visualize segmentation overlays on tissue images using the /segmentation-comparison.ipynb script
- The script already compares the outputs from the enact pipeline for default parameters

### 7. Run ENACT on VisiumHD Data using the Xenium segmentation obtained

- Save the transformed segmentation data in the data folder in which the Visium HD data is saved (find spatial/ and Binned_outputs/ folders in the same directory).
- Now you can run the ENACT pipeline with your parameters of interest (either using [SUSHI](https://fgcz-sushi.uzh.ch/) or Python). Make sure to set `expand_by_n_bins = 0`.

### 8. Final QC

- Use the //analysis/ENACT_outputs.ipynb script to have a look at the outputs. You should recognise the XEnium segmentation in the overlayed segmentation image.

# Groundingline-Greenland

## Gounding line/zone delineation using ICESat-2

This is a project of the [ICESat-2 track](https://icesat-2-2024.hackweek.io/intro.html) of the [UW Earth Sciences hackweek 2024](https://2024.hackweek.io/).

The project derives the grounding line position of Greenland's tidewater glaciers from the surface elevation measured by ICESat-2. The grounding line or grounding zone has been identified as an important feature related to the stability of tidewater glaciers. Its depth is a key parameter in modeling submarine melting. If the grounding line is above a retrograde bed, it can induce rapid retreat of the calving front. Previous studies have also shown that glaciers are more sensitive to grounding line migration than to changes in terminus position due to reductions in basal resistance. There are many other questions that need to be investigated, such as how grounding line migration might affect the drainage of subglacial channels.

During this hackweek we hope to achieve the following goals.

1. Become familiar with ICESat-2 datasets and geospatial data processing using Python.
2. Explore different methods to derive grounding lines from surface elevations.
3. Develop reproducible workflows and data visualization tools.


### Collaborators

| Name | Personal goals | Can help with | Role |
| ------------- | ------------- | ------------- | ------------- |
| Hui Gao | Testing ICESat-2's capability in deriving grounding line of Greenland tidewater glaciers | Geospatial data processing, method development, Github  | Project Lead |
| ... | ... | ... | ... |
| ... | ... | ... | ... |

### The problem

The grounding line or grounding zone is an important feature at the ice-ocean boundary. Most previous studies have focused on the Antarctic ice sheet, where large ice shelves exist. The Greenland Ice Sheet is drained by over 150 tidewater glaciers, most of which are less than 5 km wide near the terminus. Many of these glaciers terminate in a narrow fjord, and some form floating ice tongues. However, only a few datasets of the grounding lines of Greenland's tidewater glaciers are published, one of the publicly available datasets is this [CCI dataset](http://products.esa-icesheets-cci.org/products/downloadlist/GLL/) in northern Greenland. 

ICESat-2 measures surface elevation with high vertical accuracy and a small footprint. Its temporal and spatial sampling has been greatly improved compared to ICESat. However, the gaps between ground tracks and the current temporal resolution of repeated ground tracks may still not be ideal for our purpose. In addition, we can expect challenges due to tidal correction, firn correction, and uncertainty in bedrock topography.

Overall, we will test the ability of ICESat-2 to derive grounding line positions of Greenland's tidewater glaciers. Starting with data access and visualization, we will explore different methods to derive grounding lines from surface elevation. A starting point is the use of floatation height and Archimedes' principle. A demo can be found [here]().
## Data and Methods

### Data

**Key datasets**

1. **Surface elevation**: [ICESat-2 ATL06](https://nsidc.org/data/atl06/versions/6), [ICESat ATL03](https://nsidc.org/data/atl03/versions/6)
2. **Bedrock topography**: [BedMachine Greenland, Version 5](https://nsidc.org/data/idbmg4/versions/5)

**Ancillary datasets**
1. **Terminus position**: [MEaSUREs Annual Greenland Outlet Glacier Terminus Positions from SAR Mosaics, Version 2](https://nsidc.org/data/nsidc-0642/versions/2), or [TermPicks](https://doi.org/10.5281/zenodo.6557981)
2. **Satellite images**: Sentinel2 (accessed through Google Earth Engine Python API)
3. **Glacier flow lines**: [Felikson et al. (2020)](https://doi.org/10.1029/2020GL090112) (Data is available on [Zenodo](https://doi.org/10.5281/zenodo.4284759))
4. **Validation grounding line datasets**: [Ciracì et al. (2023)](https://doi.org/10.1073/pnas.2220924120) (Data is available on [Dryad](https://doi.org/10.7280/D1XT4G))

### Proposed methods/tools

We will test at least the following two different methods.

1. Calculate the floatation height using Archimedes' principle and determine whether the ice is grounded by comparing it with the surface elevation from ICESat-2.
2. Use the surface elevation profile to find the "inflexion point" ("I" in the diagram below), e.g. [Fricker and Padman et al. (2006)](https://doi.org/10.1029/2006GL026907) and [Brunt et al. (2010)](https://doi.org/10.3189/172756410791392790). This method won't need the bed topography, which has it's own uncertainty.
<img width="1205" alt="image" src="https://github.com/hui-97/Test-project/blob/main/assets/Screenshot%202024-08-12%20at%206.51.37%E2%80%AFPM.png">

Note that tidal movement or sea level variation can introduce challenges to the above mentioned methods. And none of them is a direct measurement of grounding line, but more of a proxy to the grounding line. Here is a flowchart for the proposed methods:

```mermaid
graph LR;
    A(ATL06)-->B[/Subset to AOI/];
    B-->|Method #1|C;
    B-->|Method #2|D;
    C[/Get bed elevation/]-->E[/Calculate floatation height/];
    E-->F[/Determine threshold/];
    F-->H(Grounding line);
    D(Surface elevation change profile\n along ground tracks)-->G[/Change point detection/];
    G-->H;
```

In addition, participants are welcome to explore beyond the above mentioned grounding line detection methods. Here are three examples.

**Example 1**: use ATL03 instead of ATL06 to explore the glacier gemetry near the ice-ocean boundary. One can also play with different data filtering methods to find ice surface and test if it's a better dataset for finding grounding zone, an example flowchart can be:

```mermaid
graph LR;
    A(ATL03)-->B[/Subset to AOI/];
    B-->C{is it on land ice?};
    C-->|Yes| D[/Point cloud data filtering/];
    C-->|No| E[Terminus position];
    D-->F(Ice surface);
    F-->G[/Grounding line/zone detection/]
```

**Example 2**: Data visualization is more than visualizing the data. It help us with understanding the information behind the dataset in an effective and engaging way. Tools such as *[dash](https://dash.plotly.com/)* or *[streamlit](https://streamlit.io/)* help build interactive dashboards or web apps. Objectives of trying these tools can be:

1. Visualizing 3d or 4d data without coding for users, such as showing maps, surface elevation profiles, or time series on user selected date or location.
2. Show statistics. For instance, how many glaciers on Greenland Ice Sheet have a floating ice tonge, which means the grounding line is upstream of the glacier terminus and where they are.

**Example 3**: Test using DEMs to derive grounding line and compare with ICESat-2 results. DEMs such as SPOT DEM, Arctic DEM or Worldview DEM have the potential to resolve full grounding line in the fast-flowing region of tidewater glaciers. But they do have different levels of uncertainty in their vertical accuracy, sometimes the error can be as high as a few meters. If you are interested in looking into it, even just comparing these various DEMs with ICESat-2 surface elevation, would be a great exercise.

### Additional resources or background reading

What is a ground line or grounding zone?
1. Tidewater glaciers are marine-terminating outlet glaciers, where glacier flows to the ocean with its bedrock at the terminus beneath sea level.
2. Grounding line is the boundary between grounded ice and the adjoining floating ice shelf or ice tongue ([Weertman et al., 1974](https://doi.org/10.3189/S0022143000023327)). Here is also a more recent review of "Remote sensing of glacier and ice sheet grounding lines" from [Friedl et al. (2020)](https://doi.org/10.1016/j.earscirev.2019.102948)

ICESat-2
1. Description of ICESat-2 satellite mission from [Markus et al. (2017)](https://doi.org/10.1016/j.rse.2016.12.029)
2. ICESat-2 data is available on [NSIDC](https://nsidc.org/data/icesat-2/data)
3. Python packages for obtaining ICESat-2 data: [icepyx](https://icepyx.readthedocs.io/en/latest/), [SlideRule](https://slideruleearth.io/)

Python Libraries for Geospatial Data Processing
1. [gdal](https://gdal.org/api/index.html#python-api) for general geospatial data processing.
2. [GeoPandas](https://geopandas.org/en/stable/index.html) has *GeoDataFrame* that works great with raster or vector data.
4. [Shapely](https://shapely.readthedocs.io/en/stable/) has great functions to work with vector data, such as creating and processing points, lines, and polygons.
5. [Rasterio](https://rasterio.readthedocs.io/en/stable/) has all the basin functions to read and processing raster data.
7. [pyproj](https://pyproj4.github.io/pyproj/stable/) works great for projection transformation
8. Xarray
9. hdf5, netCDF4

**Other useful tools
1. **Version control: Github and git
2. **Workflow Management System: Snakemake
3. **Interactive data display: dash, streamlit

## Project goals and tasks

### Project goals

List the specific project goals or research questions you want to answer. Think about what outcomes or deliverables you'd like to create (e.g. a series of tutorial notebooks demonstrating how to work with a dataset, results of an anaysis to answer a science question, an example of applying a new analysis method, or a new python package).

* Goal 1
* Goal 2
* ...

### Tasks

What are the individual tasks or steps that need to be taken to achieve each of the project goals identified above? What are the skills that participants will need or will learn and practice to complete each of these tasks? Think about which tasks are dependent on prior tasks, or which tasks can be performed in parallel.

* Task 1 (all team members will learn to use GitHub)
* Task 2 (team members will use the scikit-learn python library)
  * Task 2a (assigned to team member A)
  * Task 2b (assigned to team member B)
* Task 3
* ...

## Files and folders in your project repository

This template provides the following suggested organizaiton structure for the project repository, but each project team is free to organize their repository as they see fit.

* **`contributors/`**
<br> Each team member can create their own folder under contributors, within which they can work on their own scripts, notebooks, and other files. Having a dedicated folder for each person helps to prevent conflicts when merging with the main branch. This is a good place for team members to start off exploring data and methods for the project.
* **`notebooks/`**
<br> Notebooks that are considered delivered results for the project should go in here.
* **`scripts/`**
<br> Code that is shared by the team should go in here (e.g. functions or subroutines). These will be files other than Jupyter Notebooks such as Python scripts (.py).
* `.gitignore`
<br> This file sets the files that will be globally ignored by `git` for the project. (e.g. you may want git to ignore temporary files or large data files, [read more about ignoring files here](https://docs.github.com/en/get-started/getting-started-with-git/ignoring-files))
* `environment.yml`
<br> `conda` environment description needed to run this project.
* `README.md`
<br> Description of the project (see suggested headings below)
* `model-card.md`
<br> Description (following a metadata standard) of any machine learning models used in the project

## Project Results

Use this section to briefly summarize your project results. This could take the form of describing the progress your team made to answering a research question, developing a tool or tutorial, interesting things found in exploring a new dataset, lessons learned for applying a new method, personal accomplishments of each team member, or anything else the team wants to share.

You could include figures or images here, links to notebooks or code elsewhere in the repository (such as in the [notebooks](notebooks/) folder), and information on how others can run your notebooks or code.

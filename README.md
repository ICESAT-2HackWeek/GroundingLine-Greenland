# Groundingline-Greenland

## Gounding line/zone delineation using ICESat-2

This is a project of the [ICESat-2 track](https://icesat-2-2024.hackweek.io/intro.html) of [UW Earth Sciences hackweek 2024](https://2024.hackweek.io/).

The project derives the grounding line position of the Greenland tidewater glaciers from surface elevation measured by ICESat-2. The grounding line or grounding zone has been identified as an important feature that's related to tidewater glacier stabilities. Its depth is a key parameter of modeling submarine melting. When the grounding line is sitting above a retrograde bed, it can incur a fast retreat of the calving front. Previous studies have also shown that glaciers are more sensitive to grounding line migration than terminus position change due to the reduction of basal resistance. Many more questions need further investigation, such as how grounding line migration might impact the draining of subglacial channels.

During this hackweek, we hope to achieve the following objectives.

1. Get familiar with ICESat-2 datasets and processing geospatial datasets using Python.
2. Explore various methods of deriving grounding lines from surface elevation.
3. Developing reproducible workflow and data visualization tools.


### Collaborators

| Name | Personal goals | Can help with | Role |
| ------------- | ------------- | ------------- | ------------- |
| Hui Gao | Testing ICESat-2's capability in deriving grounding line of Greenland tidewater glaciers | Geospatial data processing, method development, Github  | Project Lead |
| ... | ... | ... | ... |
| ... | ... | ... | ... |

### The problem

The grounding line or grounding zone is an important feature at the ice-ocean boundary. Most previous studies focused on the Antarctica ice sheet where large ice shelves exist. Greenland ice sheet is drained by over 150 tidewater glaciers mostly with a width of less than 5 km near the terminus. Many of these glaciers terminate in a narrow fjord and some of them form floating ice tongues. However, only a few datasets of Greenland tidewater glaciers' grounding lines are published, one of the publically available datasets is this [CCI dataset](http://products.esa-icesheets-cci.org/products/downloadlist/GLL/) in northern Greenland. 

ICESat-2 measures surface elevation with high vertical accuracy and small footprint size. Its temporal and spatial sampling have been greatly improved from ICESat. However, the gaps between ground tracks and the current temporal resolution of repeated ground tracks may still not be ideal for our purpose. Moreover, we can also expect challenges due to tidal correction, firn correction, and uncertainty in bedrock topography.

Overall, we will test ICESat-2's capability of deriving grounding line positions of Greenland tidewater glaciers. We will start with data access and visualization, and explore various methods of deriving grounding lines from surface elevation. A starting point is using the floatation height and the Archimedes' principle. A demo can be found [here]().

## Data and Methods

### Data

**Key datasets**

1. **Surface elevation**: [ICESat-2 ATL06](https://nsidc.org/data/atl06/versions/6), [ICESat ATL03](https://nsidc.org/data/atl03/versions/6)
2. **Bedrock topography**: [BedMachine Greenland, Version 5](https://nsidc.org/data/idbmg4/versions/5)

**Ancillary datasets**
1. **Terminus position**: [MEaSUREs Annual Greenland Outlet Glacier Terminus Positions from SAR Mosaics, Version 2](https://nsidc.org/data/nsidc-0642/versions/2), or [TermPicks](https://doi.org/10.5281/zenodo.6557981)
2. **Satellite images**: Sentinel2
3. **Glacier flow lines**:
4. **Validation grounding line datasets**:

### Existing methods

To be added

### Proposed methods/tools

We will be at least testing the following two different methods.

1. Calculate floatation height based on Archimedes' principle and determine whether ice is grounded by comparing it with surface elevation from ICESat-2
2. Using surface elevation profile to find "flexure point", for example [Fricker and Padman et al. (2006)](https://doi.org/10.1029/2006GL026907) and [Brunt et al. (2010)](https://doi.org/10.3189/172756410791392790)
*image illustration to be added*

### Additional resources or background reading

**What's grounding line or grounding zone?**
1. citation
2. citation

**ICESat-2**
1. Citation 2017 paper
2. Link to NSIDC data portal
3. Data access packages: icepyx, SlideRule

**Python libraries for geospatial data processing**
1. gdal
2. geopandas
4. shapely
5. rasterio
7. pyproj for projection transformation
8. xarray

**Other useful tools**
1. **Version control**: Github and git
2. **Workflow management**: Snake
3. **Interactive data exhibition**: dash, streamlit

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

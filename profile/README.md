# Ines-tools

Ines-tools contains several tools for energy system modelling. The aim is to facilitate data transfers between various data formats and different model structures and to enable iterations between different modelling tools. An interoperable energy system data specification ([ines-spec](https://github.com/energy-modelling-workbench/ines-spec)) built on top of a more generic flexible data model ([spine-data-model](https://github.com/energy-modelling-workbench/spine-data-model)) have both been designed to facilitate data transfers. The system also allows to test modelling tools against an open certification process.

## Available tools
An overview of the available tools:
- an interoperable energy system data specification [ines-spec](https://github.com/energy-modelling-workbench/ines-spec) (although not a tool really, just a specification)
- data processing tools [ines-tools](https://github.com/energy-modelling-workbench/ines-tools)
- transformers between ines-spec and model specific data formats, e.g. [ines-flextool](https://github.com/energy-modelling-workbench/ines-flextool), [ines-spineopt](https://github.com/energy-modelling-workbench/ines-spineopt), [ines-osemosys](https://github.com/energy-modelling-workbench/ines-osemosys), [ines-pypsa](https://github.com/energy-modelling-workbench/ines-pypsa), [ines-empire](https://github.com/energy-modelling-workbench/ines-empire), [ines-backbone](https://github.com/ines-tools/ines-backbone)
- an open certification process [ines-certify](https://github.com/energy-modelling-workbench/ines-certify)
- a set of [data-pipelines](https://github.com/energy-modelling-workbench/data-pipelines) feeding into ines-spec

The next section shows an example of a workflow that uses these tools. The example workflow is implemented in [Spine Toolbox](https://github.com/Spine-tools/Spine-Toolbox) but not all workflows need to be implemented that way - one could also do hand-made scripts or have another GUI. However, data transformations are facilitated by ines-spec and spine-data-model and currently the only API to those is [SpineDB-API](https://github.com/spine-tools/Spine-Database-API) (that also Spine Toolbox uses under the hood).

## Example Workflow

Below you find an example of a workflow that utilizes some of the tools, code and specifications in the energy modelling workbench. The example follows the structure of data pipelines being currently built in the Mopo project at [data-pipelines](https://github.com/energy-modelling-workbench/data-pipelines) that acquire data from original sources, allow user to choose target model resolution(s), create a model in ines-spec format and then convert the data to a model specific format.

![ines workflow example](https://github.com/user-attachments/assets/583b21ae-8107-4abc-8bcc-c236b369ba44)

0. **Templates** are the prerequisites of the workflow. These are the formats/specifications of the external data, the interoperable energy system data and the models.
    + [spine-data-model](https://github.com/energy-modelling-workbench/spine-data-model) is a flexible data model that is designed to hold modelling related data. It has a graph-like structure and allows entities to hold multiple alternative values for the same data - which in turn facilitates the construction of scenarios without data repetition. It also allows to construct data structure as data. Spine Toolbox is a reference implementation of the data model and ines-spec follows the data model (hence ines-spec can use Spine Toolbox as a GUI).
    + [ines-spec](https://github.com/energy-modelling-workbench/ines-spec) contains the interoperable energy system data specification.
1. **External data sources** at the highest available resolution (geographical, temporal and technological) is used as a starting point for data acquisition. The data can come from various sources and use  different formats - data gets aggregated and converted on the way.
2. **Importers and import scripts** read external data source and deposit the data to databases. The scripts can include data clean-up and homoginization if needed.
3. **Databases for original data** follow the Spine data model (and hence allow to use functions from ines-tools in the data processing). The data specifications can follow the original data structures to a meaningful degree. This allows to capture the characteristics of that particular data while avoiding data repetition in high resolution datasets.
4. **Model builder** takes the user defined settings for the target model instance: geographical, temporal and technological resolutions for different parts of the target model. The scripts build the model instance and deposit in ines-spec conforming format.
5. **ines input data** is then a database that contains the model instance using ines-spec.
6. **ines-model converters**: to_FlexTool and to_SpineOpt are examples of scripts that convert to model specific formats and from_FlexTool and from_SpineOpt are examples of scripts that convert to ines-spec from model specific formats. These can be found in tool specific repositories like [ines-spineopt](https://github.com/energy-modelling-workbench/ines-spineopt) and [ines-flextool](https://github.com/energy-modelling-workbench/ines-flextool).
7. **Model specific databases** can be used to feed models using their own scripts like run_flextool and run_spineopt.

This is just an example, there could be further workflows that focus on a specific modelling chain or workflow that runs a certification process.

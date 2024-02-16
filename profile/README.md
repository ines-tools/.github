# Energy modelling workbench

Energy modelling workbench contains several tools for energy system modelling. These tools to deal with various data formats and different model structures. An interoperable energy system data specification (ines-spec) is central to this project.

## Available tools
An overview of the available tools:
- an interoperable energy system data specification [ines-spec](https://github.com/energy-modelling-workbench/ines-spec)
- data processing tools [ines-tools](https://github.com/energy-modelling-workbench/ines-tools)
- transformers between data formats, e.g. [ines-flextool](https://github.com/energy-modelling-workbench/ines-flextool)
- an interoperable energy system data specification [ines-spec](https://github.com/energy-modelling-workbench/ines-spec)
- an open certification process [ines-certify](https://github.com/energy-modelling-workbench/ines-certify)

The tools utilize a flexible data model [spine-data-model](https://github.com/energy-modelling-workbench/spine-data-model) that makes it easier to build data conversion tools.

The tools can be used in various ways and can be appended with your own tools and models.

The next section shows an example of a workflow using these tools. The example workflow is implemented in [Spine Toolbox](https://github.com/Spine-tools/Spine-Toolbox) but not all workflows need to be implemented that way.

## Example Workflow

Below you find an example of a workflow with the energy modelling workbench with a description of each of the processes (first level of bullet points) and the corresponding repositories in this project (second level of bullet points).

The example workflow includes (but is not limited to):
+ a first part that represents data pipelines to create high resolution data,
+ a middle part that processes the data to create data for a case study in a generic format (ines-spec) to be used by different models,
+ and a final part that represents a benchmarking comparison between two tools.

![image](https://github.com/energy-modelling-workbench/.github/blob/fb8a65d0ed3d60a964da6e11d20f8428312c2dea/profile/ines-data-tools-workflow-example.png)

0. **Templates** are the prerequisites of the workflow. These are the formats/specifications of the external data, the interoperable energy system data and the models.
    + [spine-data-model](https://github.com/energy-modelling-workbench/spine-data-model) is a flexible data model used by the tools that makes it easier to build data conversion tools.
    + [ines-spec](https://github.com/energy-modelling-workbench/ines-spec) contains the interoperable energy system data specification.
1. **External data** with the highest desired resolution is loaded into the tool. The data comes from various sources and comes in different formats.
2. **Importers** bring the external data to a more unified format. Small adjustments in the import procedure still allow to load different data in the tool when needed for a very specific study.
3. **Available data** is taken as-is as much as possible as to allow to build a wide range of scenarios later on.
4. **Data processing** is done with various tools. On one hand these tools allow to model more complex parts of the energy system to be represented by (piece-wise) linear formulations in, e.g., SpineOpt. On the other hand the tools allow to filter and aggregate data according to the scope of the study. The scenarios for the energy system model are created at this stage as well. The scenarios cover different regions, applications, levels of detail and projections.
    + [ines-tools](https://github.com/energy-modelling-workbench/ines-tools) contains some of these data processing tools.
5. **Case data** form a more specific database and considered to be ready to be used in energy system modelling tools.
6. **Exporters** translate the more general structure of the built data and scenarios to a format specific to an energy system modelling tool, e.g. SpineOpt.
    + [ines-spineopt](https://github.com/energy-modelling-workbench/ines-spineopt) translates to (and from!) [SpineOpt](https://github.com/Spine-tools/SpineOpt.jl).
    + [ines-flextool](https://github.com/energy-modelling-workbench/ines-flextool) translates to (and from!) [IRENA-flextool](https://www.irena.org/Energy-Transition/Planning/Flextool).
    + [ines-pypsa] (https://github.com/energy-modelling-workbench/ines-pypsa) translates to (and from!) [PyPSA](https://pypsa.org/).
7. **Tools** use the case data to perform the necessary calculations.
8. **Collect results** to compare the outcome of different tools.
9. **Results** contains the results of different tools in a specified format.

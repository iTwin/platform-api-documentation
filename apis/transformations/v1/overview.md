## Transformations API

The Transformations API is a service that provides an ability to transform iModel data.
A transformation process is always happening between 2 iModels. A source iModel is used as a transformation source and target iModel is used as a placeholder for transformed data.

Transformation API features:

- Filtering based on a view definition.
- Progress reporting.
- History tracking.
- Transforming changes.

Use cases:

- Project collaborators are interested in only a specific part of a project. Transformations API might be used to filter out data and produce a targeted data set.

### View Definition

A View renders geometry from one or more Models of an iModel in a web browser. A View is an element of the ViewDefinition class. More information [here](https://www.itwinjs.org/learning/frontend/views/)

## iTwin Clash Detection API
iTwin Clash Detection API checks for geometrical collision between various design element groups in the digital twin. In general terms, this involves checking if the geometrical extents of design elements are colliding or coming under clearance limits with other geometries in the digital twin. This API includes two main components: tests and results and the ability to manage them.

### Clash Tests
Clash tests define two sets of design elements based on engineering models or categories defined in the digital twin. For example, all design elements for mechanical equipment can be part of the first group, and all piping elements can be placed together in the second group.

Clash tests have advanced options for setting up clearance or suppression rules.
- Clearance around a design element. For example, all pipes must have 6in clearance for insulation requirements.
- Suppress touching with an ability to define tolerance to suppress clashes when two design elements are touching each other. For example, a steel beam and a steel column touching at the connection.
- Suppression criteria are defined based on logical rules. For example, all clashes between a wooden door and a concrete wall should be suppressed.

### Clash Results
Results are provided for each type of test. They contain clashing results for pairs of elements in the digital twin based on criteria defined in the clash test.

### Typical Clash Detection Workflow
The process for detecting clashes in iModels consists of the following steps:
- Add a clash detection test.
- Specify an iModel, version, and clash detection type.
- Designate the two sets to check against.
- Run the clash detection test.
- Retrieve and review the clash detection results.


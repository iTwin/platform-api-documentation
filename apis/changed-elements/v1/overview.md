# Changed Elements

The Changed Elements API provides consumers with the elements that have changed in an iModel between two changesets. This API has four operations:

1. Enable Change Tracking
2. Get Change Tracking
3. Get Comparison
4. Get Changesets

<img src="/images/changed-elements-overview.png" width="auto" height="150" />

Before obtaining a comparison, it is necessary to enable change tracking of an iModel. This means that the API will be listening to the following events:
1. New Named Version Created
2. Changeset Group Completed

When any of those events trigger, the API will process the new changes and store a summary of all the elements that have changed.

After tracking is enabled and the iModel is processed, the comparison endpoint may be used to query for a summary of changed elements between any two given `ChangeSets`.`

## Media links

Additional information can be found here:

* ITwin Developers Conference 2022. Changed Elements API: The Easy Way To Compare Changes - [Youtube](https://www.youtube.com/watch?v=HgpYe_oy9KY)

# Changed Elements V2

The Changed Elements API provides consumers with the elements that have changed in an iModel between two Changesets. This API has three operations:

- Create Comparison Job
- Get Comparison Job
- Delete Comparison Job

<img src="/images/changed-elements-v2-overview.png" width="auto" height="200" />

In order to get changes between the defined changeset range, follow the steps below:

1. Create a comparison job specifying a start and end Changesets IDs.
2. Get the job status.
3. Once the job is completed the status response will contain the comparison information.

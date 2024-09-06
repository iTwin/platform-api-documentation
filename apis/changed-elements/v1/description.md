# Changed Elements

The Changed Elements API provides consumers with the elements that have changed in an iModel between two changesets.

Operations Include:

- [Create Comparison Job](operations/create-comparison-job/) Creates a comparison. The comparison will be queued when first created and will progress to completion. When completed, it will contain all the comparison info. Use [Get Comparison Job](operations/get-comparison-job/) for information on comparison.

- [Delete Comparison Job](operations/delete-comparison-job/) Deletes all stored data relating to comparison. 

- [Get Comparison Job](operations/get-comparison-job/) Gets comparison based on the job id. The comparison will contain the job status, start and end changeset ids, and comparison progress. If the comparison is complete, the response will also include a href to the comparison information.

## Storage API

The Storage API enables the ability to access and manage files stored in the cloud and associated with a project. Organize files in a hierarchical structure with folders. Add sub-folders for additional structure, if needed.

The root folder is an entry point for using the Storage API. There are two ways to retrieve it.

- By [getting project iTwin](/apis/itwins/operations/get-itwin/)
- By [getting top-level folders and files](/apis/storage/operations/get-top-level-folders-and-files-by-project/).

Both responses include the link to the root folder.

### Things you can do with the Storage API

- Synchronize files from Storage to an iModel. Review the [Synchronize a file from iTwin Storage](/tutorials/synchronization-storage-tutorial/) tutorial for more information.
- Export issues and forms as pdf files to Storage. Review the [Export issues to Storage](/apis/issues-v1/operations/export-issues-to-storage/) and [Export forms to Storage](/apis/forms/operations/export-form-to-storage/) APIs.
- Access the [Get started with Storage API](/tutorials/storage-quick-start/) guide to start working with the Storage API.

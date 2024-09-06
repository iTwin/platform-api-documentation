# Saved Views API

This API provides functionality to store, share, organize, and retrieve saved views.

## Saved Views

Saved views enable applications to maintain display information on how to visualize an iTwin. The information stored in a saved view depends on its type. A saved view relates to an iTwin.js view definition, which comes in three different flavors:

- **3D View**: these views include camera position, camera angle, camera extents, viewed categories and viewed models.
- **Drawing Views**: these views include the origin of the view, angles, the model being viewed and the viewed categories.
- **Sheet Views**: these views include all the information from drawing views, and includes optional width, height, scale and sheet related properties, like sheet attachments.

Saved views can be shared, have thumbnails, be organized into groups, and have a list of user-defined tags.

Saved views are always related to a specific iTwin or a specific Project.

## Thumbnails

The API has operations to upload and get images related to a specific saved view. These images are typically used as thumbnails to show how the saved view looks when visualizing it. You can request the images in two sizes: `full` and `thumbnail`.

## Groups

The API allows for the creation of Groups that can be used to organize collections of saved views. Groups can be shared if desired. The user can then query saved views that are associated with a specific group by using its id.

## Tags

The API allows for marking saved views with user-created tags. Tags are simple strings that users can use for organization purposes.

## Permissions

Users have access to Saved Views as long as they have access to the iModel or iTwin they are querying.

Shared Views can be read by all users that have access to the iModel or iTwin. A view is considered shared, if the `shared` field in its data is `true`. A user cannot edit or delete another user's shared saved view.

For more control, you can use the [Access Control API](https://developer.bentley.com/apis/access-control/). In the `Saved Views` category in permissions, assign the `Manage` permission. This permission allows the user to:
1. Delete and update shared saved views
2. Delete and update shared groups
3. Delete and update shared saved views' extensions
4. Update shared saved views' thumbnails
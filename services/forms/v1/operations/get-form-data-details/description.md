---

Retrieves all properties of the specified form data instance.

Known, common properties will be returned directly on the 'formData' object, whereas custom properties unique to the form's type will be returned on the 'properties' sub-object.

Note that many properties in the schema are described as 'Origin info.' This means that they are metadata about where the form data came from and what business domain object(s) it is related to, such as a PDF file or a 3D model. Their meanings can differ from application to application. Many applications will use only a subset of these properties, and in general applications SHOULD NOT use or set these values unless they have a good reason to do so. Other properties, not marked 'Origin info', are defined for all form types, but clients SHOULD NOT assume that all of them are set.

### Permissions

To use this endpoint, the user is required to have the Forms **View** (`Forms_ViewAccess`) permission for the iTwin, or for the form's definition if form definition security is specified. (Having any other Forms permission automatically grants the **View** permission as well.)

{!Authorization.md!}

---
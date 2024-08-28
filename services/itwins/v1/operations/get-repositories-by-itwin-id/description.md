---

Gets the details of the specified repository.

A repository is a Uri link to iTwin data managed by another service.

For example, if an iTwin has Forms data then you can get the Uri for that
data by using this api and specifying iTwinId = 547d397a-9921-4e4f-a7a2-c47fc19219b0 and Class = Forms. It will return the following.
```
{
   "repositories": [
   {
      "id": "547d397a-9921-4e4f-a7a2-c47fc19219b0",
      "class": "Forms",
      "subClass": null,
      "uri": "https://api.bentley.com/forms?projectId=547d397a-9921-4e4f-a7a2-c47fc19219b0"
   }]
}
```
If no Class is specified then all repositories containing data for the iTwin will be returned. The Uri is automatically generated
by calling each service to determine if its repository contains data for the specified iTwin. For example, if there are no iModels for the specified iTwin
then the iModel Repository Uri will not be returned. 

The following Classes/SubClasses are supported. Classes in italics are auto generated. The others can be added manually using the POST endpoint.
- *iModels*
- *RealityData*
- *Storage*
- *Forms*
- *Issues* 
- *SensorData* 
- GeographicInformationSystem
	+ WebMapService
    + WebMapTileService
    + MapServer
- Construction
    + Performance 
- Subsurface
    + EvoWorkspace 

{!Authorization.md!}

### Authorization

User must be an Organization Administrator for the Organization that owns the specified iTwin Repository or be an iTwin team member.

An Organization Administrator must have at least one of the following roles assigned in User Management: Account Administrator, Co-Administrator, or CONNECT Services Administrator. For more information about User Management please visit our Bentley Communities [Licensing, Cloud, and Web Services](https://bentleysystems.service-now.com/community?id=kb_article_view&sys_kb_id=1e5410491b7d8a90f3fc5287624bcb57) wiki page.

---

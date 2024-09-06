The **iTwin Entities Service** manages a registry of the real-world entities of business significance for an iTwin, thus recording the *subject matter* of the iTwin. Each entity record has links to representations of the entity-of-business-significance in iTwin native and 3rd party services. These links point to records in content repositories that describe and inform the entity.

The Entities Service serves as the entry point for an iTwin Application to discover the content of an iTwin. Each entity record serves as the *hub* and the links as the *spokes* in a hub-and-spoke pattern relating records in different content repositories to each other.

The **Entities Service** is a form of *digital thread* that ties together data from multiple repositories into a cohesive, multi-faceted representation of the subject matter of the iTwin. It classifies, identifies, and organizes the subject matter Entities in a way that makes sense to end-users of the iTwin. It also uses the Entity records to index the iTwin's content resources and map disparate content.

<img src="/images/entities-service-overview.png" />

A real-world entity *of business significance* typically has a formal identifier or *code*, a human-readable identifier that encodes some business meaning for users. Examples include Asset Number, Room Number, Building Number, Document Code, Tag Numbers, and more.

Conversely, if an entity has no identifier that users could recognize and interpret, it typically is not of significance to the business. The entities will typically be physical assets or locations. They could also represent events or ongoing or repeating processes. In this way, the Entities Service acts as an Asset Registry, Location Registry, and possibly some other high-level registries. Only users of the iTwin can definitively say which entities are significant to them.
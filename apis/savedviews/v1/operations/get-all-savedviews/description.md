---

Retrieves all saved view associated to a iTwin, iTwin/iModel combination or group, at least one parameter must be provided.

This operation supports pagination and will sort saved views by displayName.

As the view data can be quite large, this collection call will not contain the view data themselves. To retrieve the data, make a call to [Get saved view](../get-savedview)

Extension data is returned as a list of links to query further. If you want to obtain the full saved view data, including extension data, use the `Prefer` header with `return=representation`.

{!Authorization.md!}

---

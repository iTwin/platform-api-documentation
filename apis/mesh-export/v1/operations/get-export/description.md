---

Retrieves the information for a single export. Exports are persisted until deleted.

When a mesh export succeeds, the `_links.mesh` returns a URL to download the resulting mesh from the blob container. You can list the contents of the container by appending the query parameters `restype=container&comp=list` to the URL. Note: Anyone with this URL has access to download the resultant mesh, share with care. The link is valid for one hour.

### GLTF Meshes

Exporting `GLTF` meshes produces two files: `Export.gltf` and `Export.bin`. To download these files you must split the URL provided in `_links.mesh.href` and append the file name to the URL before the query parameters. For example:
`SASUrl/Export.gltf?SASKey` and `SASURL/Export.bin?SASKey`. Use these URLs to download the relevant files. Note: The files will always be named `Export.gltf` and `Export.bin`.

### 3DFT Meshes

When exporting `3DFT` meshes, feed the URL to the [Unreal Engine Plugin](https://github.com/iTwin/unreal-engine-3dft-plugin) to stream the mesh in Unreal.

{!Authorization.md!}

---

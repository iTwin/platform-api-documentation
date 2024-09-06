## Mesh Export API

<div style="width: fit-content;">

<img src="/images/mesh-export-overview.png" alt="Export your iModel data to build visualization experiences." style="width: 100%"/>

<div style="width: 100%" align="center">

Export your iModel data to build visualization experiences.

</div>
</div>

### Present 3D scenes in game or rendering engines

The Mesh Export API makes your iModel data available in the format required by external visualization platforms such as Three.js, Unity, Unreal Engine, and other rendering platforms. Currently, the API supports exporting [glTF files](https://www.khronos.org/gltf/) and our own `3DFT` proprietary format for streaming graphics into Unreal Engine using our [Unreal Engine Plugin](https://github.com/iTwin/unreal-engine-3dft-plugin).

Features:

1. Export meshes from the latest or any specific version of the iModel.
1. Limit the scope of the exported mesh using filters and options. Note: This is only available for `GLTF` exports currently.
1. Download and stream exported files.

This API produces two types of meshes:

1. [glTF 2.0 binary files](https://www.khronos.org/gltf/) with embedded textures.
1. 3DFT 1.0 binary files for direct streaming. Note: This is only available for Unreal Engine currently.

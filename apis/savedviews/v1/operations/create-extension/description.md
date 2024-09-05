---

Creates an extension that contains custom data in a saved view.

Extensions allow a saved view to be enhanced with custom data. The extensions have to be defined in a proprietary .JSON schema file. For now, only three extensions are available:
## Extension Schemas
The following extensions are available and are shown below in the details sections.
The details sections contain the schema followed by an example of that schema.
### Per Model Category Visibility - Schema
<details>
    <summary>Per Model Category Visibility Details</summary>
```
[
   {
   "type": "array",
   "name": "perModelCategoryVisibilityProps",
   "required": true,
      "items": {
         "type": "object",
         "required": true,
         "properties": [
            {
               "name": "modelId",
               "type": "Id64String",
               "required": true
            },
            {
               "name": "categoryId",
               "type": "Id64String",
               "required": true
            },
            {
               "name": "visible",
               "type": "boolean",
               "required": true
            }            
         ]
      }
   }
]
```
Per Model Category Visibility - Example
```
{
  "perModelCategoryVisibilityProps": [
    {
      "modelId": "0x20000000079",
      "categoryId": "0x2000000003e",
      "visible": true
    },
    {
      "modelId": "0x20000000079",
      "categoryId": "0x2000000004e",
      "visible": false
    }
  ]
}
```
</details>
### Emphasize Elements - Schema
<details>
    <summary>Emphasize Elements Details</summary>
```
[
   {
   "type": "object",
   "name": "emphasizeElementsProps",
   "required": true,
      "properties": [
         {
            "name": "neverDrawn",
            "type": "array",
            "required": false,
            "items": {
               "type": "Id64String"
            }         
         },
         {
            "name": "alwaysDrawn",
            "type": "array",
            "required": false,
            "items": {
               "type": "Id64String"
            }         
         },
         {
            "name": "isAlwaysDrawnExclusive",
            "type": "boolean",
            "required": false
         },
         {
            "name": "alwaysDrawnExclusiveEmphasized",
            "type": "array",
            "required": false,
            "items": {
               "type": "Id64String"
            }         
         },
         {
            "name": "defaultAppearance",
            "type": "object",
            "required": false,
            "properties": [
               {
                  "name": "rgb",
                  "type": "object",
                  "properties": [
                     {
                        "name": "r",
                        "type": "number",
                        "required": true
                     },
                     {
                        "name": "g",
                        "type": "number",
                        "required": true
                     },
                     {
                        "name": "b",
                        "type": "number",
                        "required": true
                     }
                  ]
               },
               {
                  "name": "weight",
                  "type": "number"
               },
               {
                  "name": "transparency",
                  "type": "number"
               },
               {
                  "name": "viewDependentTransparency",
                  "type": "boolean"
               },
               {
                  "name": "linePixels",
                  "type": "integer"
               },
               {
                  "name": "ignoresMaterial",
                  "type": "boolean"
               },
               {
                  "name": "nonLocatable",
                  "type": "boolean"
               },
               {
                  "name": "emphasized",
                  "type": "boolean"
               }
            ]
         },
         {
            "name": "appearanceOverride",
            "type": "array",
            "items": {
               "type": "object",
               "properties": [
                  {
                     "name": "overrideType",
                     "type": "integer"
                  },
                  {
                     "name": "color",
                     "type": "number"
                  },
                  {
                     "name": "ids",
                     "type": "array",
                     "items": {
                        "type": "Id64String"
                     }
                  }
               ]
            }
         },
         {
            "name": "wantEmphasis",
            "type": "boolean"
         },
         {
            "name": "unanimatedAppearance",
            "type": "object",
            "required": false,
            "properties": [
               {
                  "name": "rgb",
                  "type": "object",
                  "properties": [
                     {
                        "name": "r",
                        "type": "number",
                        "required": true
                     },
                     {
                        "name": "g",
                        "type": "number",
                        "required": true
                     },
                     {
                        "name": "b",
                        "type": "number",
                        "required": true
                     }
                  ]
               },
               {
                  "name": "weight",
                  "type": "number"
               },
               {
                  "name": "transparency",
                  "type": "number"
               },
               {
                  "name": "viewDependentTransparency",
                  "type": "boolean"
               },
               {
                  "name": "linePixels",
                  "type": "integer"
               },
               {
                  "name": "ignoresMaterial",
                  "type": "boolean"
               },
               {
                  "name": "nonLocatable",
                  "type": "boolean"
               },
               {
                  "name": "emphasized",
                  "type": "boolean"
               }
            ]
         }
      ]
   }
]
```
Emphasize Elements - Example
```
{
  "emphasizeElementsProps": {
    "neverDrawn": [
      "0x20000003865",
      "0x20000003864",
      "0x200000055e4",
      "0x200000055e3",
      "0x200000039af",
      "0x200000039ae"
    ]
  }
}
```
</details>
### Visibility Override - Schema
<details>
    <summary>Visibility Override Details</summary>
```
[
   {
      "name": "visibilityOverrideProps",
      "type": "object",
      "required": true,
      "properties": [
        {
          "name": "subCategoryOverrides",
          "type": "array",
          "items": {
            "type": "object",
            "properties": [
              {
                "name": "ids",
                "type": "array",
                "required": true,
                "items": {
                  "type": "Id64String"
                }
              },
              {
                "name": "app",
                "type": "object",
                "required": true,
                "properties": [
                  {
                    "name": "rgb",
                    "type": "object",
                    "properties": [
                      {
                        "name": "r",
                        "type": "number",
                        "required": true
                      },
                      {
                        "name": "g",
                        "type": "number",
                        "required": true
                      },
                      {
                        "name": "b",
                        "type": "number",
                        "required": true
                      }
                    ]
                  },
                  {
                    "name": "weight",
                    "type": "number"
                  },
                  {
                    "name": "transparency",
                    "type": "number"
                  },
                  {
                    "name": "viewDependentTransparency",
                    "type": "boolean"
                  },
                  {
                    "name": "linePixels",
                    "type": "integer"
                  },
                  {
                    "name": "ignoresMaterial",
                    "type": "boolean"
                  },
                  {
                    "name": "nonLocatable",
                    "type": "boolean"
                  },
                  {
                    "name": "emphasized",
                    "type": "boolean"
                  }
                ]
              }
            ]
          }
        },
        {
          "name": "modelOverrides",
          "type": "array",
          "items": {
            "type": "object",
            "properties": [
              {
                "name": "ids",
                "type": "array",
                "required": true,
                "items": {
                  "type": "Id64String"
                }
              },
              {
                "name": "app",
                "type": "object",
                "required": true,
                "properties": [
                  {
                    "name": "rgb",
                    "type": "object",
                    "properties": [
                      {
                        "name": "r",
                        "type": "number",
                        "required": true
                      },
                      {
                        "name": "g",
                        "type": "number",
                        "required": true
                      },
                      {
                        "name": "b",
                        "type": "number",
                        "required": true
                      }
                    ]
                  },
                  {
                    "name": "weight",
                    "type": "number"
                  },
                  {
                    "name": "transparency",
                    "type": "number"
                  },
                  {
                    "name": "viewDependentTransparency",
                    "type": "boolean"
                  },
                  {
                    "name": "linePixels",
                    "type": "integer"
                  },
                  {
                    "name": "ignoresMaterial",
                    "type": "boolean"
                  },
                  {
                    "name": "nonLocatable",
                    "type": "boolean"
                  },
                  {
                    "name": "emphasized",
                    "type": "boolean"
                  }
                ]
              }
            ]
          }
        },
        {
          "name": "catEmphasizeOverride",
          "type": "object",
          "properties": [
            {
              "name": "ids",
              "type": "array",
              "required": true,
              "items": {
                "type": "Id64String"
              }
            },
            {
              "name": "app",
              "type": "object",
              "required": true,
              "properties": [
                {
                  "name": "rgb",
                  "type": "object",
                  "properties": [
                    {
                      "name": "r",
                      "type": "number",
                      "required": true
                    },
                    {
                      "name": "g",
                      "type": "number",
                      "required": true
                    },
                    {
                      "name": "b",
                      "type": "number",
                      "required": true
                    }
                  ]
                },
                {
                  "name": "weight",
                  "type": "number"
                },
                {
                  "name": "transparency",
                  "type": "number"
                },
                {
                  "name": "viewDependentTransparency",
                  "type": "boolean"
                },
                {
                  "name": "linePixels",
                  "type": "integer"
                },
                {
                  "name": "ignoresMaterial",
                  "type": "boolean"
                },
                {
                  "name": "nonLocatable",
                  "type": "boolean"
                },
                {
                  "name": "emphasized",
                  "type": "boolean"
                }
              ]
            }
          ]
        },
        {
          "name": "modelEmphasizeOverride",
          "type": "object",
          "properties": [
            {
              "name": "ids",
              "type": "array",
              "required": true,
              "items": {
                "type": "Id64String"
              }
            },
            {
              "name": "app",
              "type": "object",
              "required": true,
              "properties": [
                {
                  "name": "rgb",
                  "type": "object",
                  "properties": [
                    {
                      "name": "r",
                      "type": "number",
                      "required": true
                    },
                    {
                      "name": "g",
                      "type": "number",
                      "required": true
                    },
                    {
                      "name": "b",
                      "type": "number",
                      "required": true
                    }
                  ]
                },
                {
                  "name": "weight",
                  "type": "number"
                },
                {
                  "name": "transparency",
                  "type": "number"
                },
                {
                  "name": "viewDependentTransparency",
                  "type": "boolean"
                },
                {
                  "name": "linePixels",
                  "type": "integer"
                },
                {
                  "name": "ignoresMaterial",
                  "type": "boolean"
                },
                {
                  "name": "nonLocatable",
                  "type": "boolean"
                },
                {
                  "name": "emphasized",
                  "type": "boolean"
                }
              ]
            }
          ]
        }
      ]
   }
]
```
Visibility Override - Example
```
{
  "visibilityOverrideProps": {
    "subCategoryOverrides": [
      {
        "ids": [
          "0x200000009e5",
          "0x20000000a45"
        ],
        "app": {
          "rgb": {
            "r": 12,
            "g": 12,
            "b": 107
          },
          "transparency": 0.46
        }
      },
      {
        "ids": [
          "0x20000007771",
          "0x20000007810"
        ],
        "app": {
          "rgb": {
            "r": 12,
            "g": 12,
            "b": 107
          },
          "transparency": 0.46
        }
      }
    ]
  }
}
```
</details>

Later on, consumers of the API will be allowed to define their own extensions.

{!Authorization.md!}

---

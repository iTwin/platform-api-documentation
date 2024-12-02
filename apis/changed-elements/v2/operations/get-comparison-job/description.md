---

Gets comparison based on the job Id, iTwin Id, and iModel Id. The comparison will contain the job status, start and end changeset ids, and comparison progress. If the comparison is complete, the response will also include an href to the comparison information.

Job Id: is normally comprised of start changeset id and end changeset id, in the following format: {startChangesetId}-{endChangesetId}

### Understanding Change

The comparison job blob, which can be downloaded using the provided link, includes a [ChangedElements](https://www.itwinjs.org/reference/core-common/entities/changedelements/) object. This object comprises several arrays of identical size. Each element across these arrays is identified by a unique index.
map

Here are some key arrays that provide insights into the modifications made to an element:

**opcodes**: This array stores operation codes that indicate whether an element was inserted, updated, or deleted during the change. For more details, refer to [DbOpcode](https://www.itwinjs.org/reference/core-bentley/besqlite/dbopcode/). The relevant values are outlined below:

| Opcode | Description |
|:------:|-----------|
| 9 | Element was deleted |
| 23 | Element was modified |
| 18 | Element was inserted |

&nbsp;
&nbsp;

**type**: Contains the type of change that occurred to the element. This number is a bit-flag and can be used to know whether the element had property changes, geometric changes, placement changes, indirect changes, and hidden property changes. See [TypeOfChange](https://www.itwinjs.org/reference/core-common/entities/typeofchange/) for more information. Below is a table with the values and their meaning:

| Type | Value | Description |
|------|:-----:|-------------|
| Property | 1 | A property in the element changed |
| Geometry | 2 | The geometry of the element changed |
| Placement | 4 | The placement of the element changed. This means that the element changed its volume, origin or rotation. |
| Indirect | 8 | Indirect change occurred to this element by a related instance that provides properties for it |
| Hidden | 16 | Hidden properties of the element changed |
| Parent | 32 | The top-most parent of the element has changed |

### Prefer Header

You may set the `Prefer` header as `return=minimal` if you want to skip all data related to element properties.

{!Authorization.md!}
---

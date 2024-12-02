---

Use this request to look up a list group, which is a nested object structure that defines the options available in a chain of cascading list form controls. (Cascading lists are a set of &lt;select&gt; elements where only the first one is initially enabled until an option in it is selected, and then, depending on which option was selected, the available options in the next list can vary.) Each property in the structure represents an option in a select list, and its children represent options that become available in the next list in the chain if that option is selected.

### Sample Explanation

The sample for the 200 response shows an example of a list group that could be assigned to 3 controls in a form to let the user pick an American football team by conference, division, and name. Since the result has two properties ("AFC" and "NFC") as direct children of the "optionsTree" property, the first list in the cascading list chain would have two options--"AFC" and "NFC".  Whichever option is chosen, its child properties become available for selection in the second list, and so forth.  For example, if "AFC" and "North" were chosen for the first two lists respectively, the third list would show the available options "Bengals", "Browns", "Ravens", and "Steelers".  These four properties just have empty objects as their values because this particular list group only has three layers; these options are the final options in the chain and have no descendants.

{!Authorization.md!}

---
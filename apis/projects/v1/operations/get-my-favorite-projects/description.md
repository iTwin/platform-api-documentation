---

Retrieves a list of favorite projects for the logged in user. The user is determined by the authentication token.

{!ProjectsDeprecated.md!}

{!Authorization.md!}

### Response

By default, each project in the returned list of projects will have only the project id, display name and project number.

A full representation of each project can be returned by specifying the *prefer* header that includes a value of *return=representation*.

---

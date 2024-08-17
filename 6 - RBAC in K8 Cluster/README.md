# Role Based Access Control in Kubernetes Cluster

Kubernetes Role-Based Access Control (RBAC) is a mechanism that helps manage and restrict user access to resources within a Kubernetes cluster. 

It allows administrators to define who can access which resources and what actions they can perform on those resources.

## Roles and ClusterRoles

**Role:** Defines a set of permissions within a specific namespace. It contains rules that specify what actions can be performed on which resources.

**ClusterRole:** Similar to a Role but applies across the entire cluster, not limited to a specific namespace. It can be used for cluster-wide resources or to define global permissions.

## RoleBindings and ClusterRoleBindings:**

**RoleBinding:** Associates a Role with users, groups, or service accounts within a specific namespace. It grants the permissions defined in the Role to the specified subjects within that namespace.

**ClusterRoleBinding:** Associates a ClusterRole with users, groups, or service accounts across the entire cluster. It grants the permissions defined in the ClusterRole cluster-wide.

## Subjects:

These are the entities (users, groups, or service accounts) that are granted permissions through Roles or ClusterRoles.

## Resources and Verbs:

**Resources:** Kubernetes objects like pods, deployments, services, etc.

**Verbs:** Actions that can be performed on resources, such as get, list, create, update, delete, etc.

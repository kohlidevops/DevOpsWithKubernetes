# Scaling Application in Kubernetes using Replication Controller

**App Scaling**

➢ Application scalability is the potential of an application to grow in time, being able to efficiently handle more and more requests per minute (RPM).

➢ In kubernetes, user can scale Pods.

➢ Pods can be scale Vertically or Horizontally.

**Stateless Applications**

➢ A stateless application is one that does not store client data from one session to the next. Each request from a client is handled independently, and no session information is retained between different requests.

➢ Stateless applications can be scaled horizontally, meaning new instances (Pods) can be created to handle more load without any dependency on previous requests.

_Examples:_ Web servers, front-end applications.

**Stateful Applications**

➢ A stateful application is one that remembers client data (session information or state) across requests. The state of the application (such as database connections or user session data) is maintained even after the session ends.

➢ Stateful applications are typically scaled vertically (adding more resources to a single instance). However, stateful workloads can also be scaled horizontally with careful orchestration of persistent storage.

_Examples:_ Databases (e.g., MySQL, MongoDB), distributed systems like Kafka or Redis.

**Scaling in Kubernetes**

➢ ReplicationController can be used to manage the App Scaling.

➢ ReplicationController ensures that a specified number of pod replicas are running at any point of time.

➢ ReplicationController makes sure that a pod or a set of pods is always up and available.


# Kubernetes Persistent Volumes (PV) & Persistent Volume Claims (PVC)

Kubernetes supports the configuration of persistent storage through Persistent Volumes (PV) and Persistent Volume Claims (PVC). This system allows for the storage and management of data beyond the lifecycle of individual pods, ensuring data persistence across pod restarts and deployments.

## Persistent Volume (PV)

A Persistent Volume (PV) in Kubernetes is a piece of storage in the cluster that has been provisioned by an administrator or dynamically by the system. It functions similarly to a network disk that the cluster can utilize to store data persistently, thereby allowing the data to survive beyond the life of individual pods.

## Persistent Volume Claim (PVC)

A Persistent Volume Claim (PVC) is essentially a storage request made by a user. It acts like an order for a specific size and type of storage, which can then be fulfilled by matching it with an appropriate Persistent Volume. The PVC specifies the required size and, sometimes, the type of storage, facilitating an appropriate match with a PV.

## Use Cases in Real Time

- **Database Storage**: PVs can be used to store database files, ensuring that the database service can be restarted or migrated across pods without data loss.
- **File Storage for Web Applications**: For web applications that allow file uploads, using PVs ensures that uploaded files remain accessible, even if the serving pod is restarted.
- **Logging and Monitoring Data**: PVs are ideal for logging and monitoring applications that accumulate data over time, allowing for the retention and analysis of logs even if the collecting pods are replaced.

## Interview Questions and Answers

### 1. What is the difference between a PV and a PVC?

- **Answer**: A PV is storage provisioned by an administrator or dynamically by the system, akin to a hard drive for the cluster. A PVC is a request for storage from a user, specifying size and access modes, acting as an order form that needs to be filled by a PV.

### 2. How does Kubernetes match a PVC to a PV?

- **Answer**: Kubernetes matches a PVC to a PV based on labels, size, and access modes, ensuring a PV with sufficient size and the requested access modes is found. If a suitable PV with matching labels is found, the PVC is bound to it.

### 3. Can a PV be used by multiple PVCs?

- **Answer**: Generally, a PV is bound to a single PVC. However, Kubernetes supports storage types that allow multiple PVCs to access a PV simultaneously, using ReadWriteMany or RWX access modes, depending on the storage system's capabilities.

### 4. What happens to the data on a PV when a PVC is deleted?

- **Answer**: By default, the PV is retained and the data remains on the PV even after the PVC is deleted. This behavior can be configured to automatically delete the PV or recycle it for new PVCs, but recycling might not securely erase the data.

### 5. How can you dynamically provision PVs?

- **Answer**: Kubernetes enables dynamic provisioning of PVs through StorageClasses, which define the provisioner and parameters for creating new PVs. When a PVC specifies a StorageClass, a new PV that fulfills the request is automatically created, eliminating manual administrator intervention.


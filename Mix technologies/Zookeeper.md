- Zookeeper
	- Zookeeper is an open source distributed coordination service that helps to manage a large set of hosts. Management and coordination in a distributed environment is tricky. Zookeeper automates this process and allows developers to focus on building software features rather than worry about it’s distributed nature.
	- Zookeeper helps you to maintain configuration information, naming, group services for distributed applications. It implements different protocols on the cluster so that the application should not implement on their own. It provides a single coherent view of multiple machines.
- ZooKeeper Architecture:
	- Apache ZooKeeper is a coordination service for distributed applications. It aims to solve the tough problems associated with the coordination of components in a distributed application. It does this by exposing a simple yet powerful interface of primitives. Applications can be designed on these primitives implemented through ZooKeeper APIs to solve the problems of distributed synchronization, cluster configuration management, group membership, and so on.
	- ZooKeeper is, in itself, a replicated and distributed application, with the intention to be run as a service, similar to the way we run DNS or any other centralized service.
	- Zookeeper follows a Client-Server Architecture
		- Server: The server sends an acknowledge when any client connects. In the case when there is no response from the connected server, the client automatically redirects the message to another server.
		- Client: Client is one of the nodes in the distributed application cluster. It helps you to accesses information from the server. Every client sends a message to the server at regular intervals that helps the server to know that the client is alive.
		- Leader: One of the servers is designated a Leader. It gives all the information to the clients as well as an acknowledgment that the server is alive. It would performs automatic recovery if any of the connected nodes failed.
    - All systems store a copy of the data
    - Leaders are elected at startup
    	- Follower: Server node which follows leader instruction is called a follower.
			- Client read requests are handled by the correspondingly connected Zookeeper server
    		- The client writes requests are handled by the Zookeeper leader.
    	
    		![Screenshot 2022-09-03 at 12 31 42 PM](https://user-images.githubusercontent.com/49789867/188262166-852bc483-abe9-4811-bf95-6f8609ac1422.png)
- The Zookeeper Data Model:
	- The zookeeper data model follows a Hierarchal namespace where each node is called a ZNode. A node is a system where the cluster runs.
	- Every ZNode has data. It may or may not have children
	- ZNode paths: 
		- Canonical, slash-separated and absolute
    	- Not use any relative references
    	- Names may have Unicode characters
    
    	![Screenshot 2022-09-03 at 12 31 26 PM](https://user-images.githubusercontent.com/49789867/188262177-1b392ba5-fa65-406e-9aff-8f47b55a4fba.png)
- The ZKS – Session States and Lifetime
	- Before executing any request, it is important that the client must establish a session with service
    - All operations clients are sent to service are automatically associated with a session
    - The client may connect to any server in the cluster. But it will connect to only a single server
    - The session provides “order guarantees”. The requests in the session are executed in FIFO order
    - The main states for a session are 1) Connecting, 2) Connected 3) Closed 4) Not Connected.
- Keeping an eye on znode changes:
	- ZooKeeper is designed to be a scalable and robust centralized service for very large distributed applications. A common design anti-pattern associated while accessing such services by clients is through polling or a pull kind of model. A pull model often suffers from scalability problems when implemented in large and complex distributed systems. To solve this problem, ZooKeeper designers implemented a mechanism where clients can get notifications from the ZooKeeper service instead of polling for events. 
	- Clients can register with the ZooKeeper service for any changes associated with a znode. This registration is known as setting a watch on a znode in ZooKeeper terminology. Watches allow clients to get notifications when a znode changes in any way. A watch is a one-time operation, which means that it triggers only one notification. To continue receiving notifications over time, the client must reregister the watch upon receiving each event notification.
	- Example:
		- In the cluster, a node, say Client1, is interested in getting notified when another node joins the cluster. Any node that is joining the cluster creates an ephemeral node in the ZooKeeper path /Members.
		- Now, another node, Client2, joins the cluster and creates an ephemeral node called Host2 in /Members.
		- Client1 issues a getChildren request on the ZooKeeper path /Members, and sets a watch on it for any changes. When Client2 creates a znode as /Members/Host2, the watch gets triggered and Client1 receives a notification from the ZooKeeper service. 
		-  If Client1 now issues getChildren request on the ZooKeeper path /Members, it sees the new znode Host2. This flow of the setting of watches, and notifications and subsequent resetting of the watches












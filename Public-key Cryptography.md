```mermaid
architecture-beta
    %% =========================
    %% Federated Learning (FL)
    %% =========================

    group server(cloud)[Central Server]
		service database(database)[Database] in server
	
	group client(database)[Clients]
		service database(database2)[Database] in client

```
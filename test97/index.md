---
title: "Troubleshoot connecting to the SQL Server Database Engine | Microsoft Docs"
ms.custom: sqlfreshmay19
ms.date: "11/25/2019"
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ""
ms.technology: configuration
ms.topic: troubleshooting
helpviewer_keywords: 
  - "troubleshooting, connecting to Database Engine"
  - "connecting to Database Engine, troubleshooting"
ms.assetid: 474c365b-c451-4b07-b636-1653439f4b1f
author: MikeRayMSFT
ms.author: mikeray
---


1. On the client computer, using SQL Server Management Studio, attempt to connect using the IP Address and the TCP port number in the format IP address comma port number. For example, `192.168.1.101,1433`. If this connection fails, then you probably have one of the following problems:

   - `ping` of the IP address doesn't work, indicating a general TCP configuration problem. Go back to the section [Testing TCP/IP connectivity](#testTCPIP).
   - SQL Server is not listening on the TCP protocol. Go back to the section [Enable protocols](#enableprotocols).
   - SQL Server is listening on a port other than the port you specified. Go back to the section [Get the TCP port number](#getTCP).
   - The SQL Server TCP port is being blocked by the firewall. Go back to the section [Open a port in the firewall](#open-a-port-in-the-firewall).

2. Once you can connect using the IP address and port number, attempt to connect using the IP address without a port number. For a default instance, just use the IP address. For a named instance, use the IP address and the instance name in the format IP address backslash instance name, for example `192.168.1.101\<instance name>` If this doesn't work, then you probably have one of the following problems:

   - If you are connecting to the default instance, it might be listening on a port other than TCP port 1433, and the client isn't attempting to connect to the correct port number.
   - If you are connecting to a named instance, the port number is not being returned to the client.

   Both of these problems are related to the SQL Server Browser service, which provides the port number to the client. The solutions are:

   - Start the SQL Server Browser service. See the instructions to [start browser in SQL Server Configuration Manager](#startbrowser).
   - The SQL Server Browser service is being blocked by the firewall. Open UDP port 1434 in the firewall. Go back to the section [Open a port in the firewall](#open-a-port-in-the-firewall). Make sure you are opening a UDP port, not a TCP port.
   - The UDP port 1434 information is being blocked by a router. UDP communication (user datagram protocol) is not designed to pass through routers. This keeps the network from getting filled with low-priority traffic. You might be able to configure y

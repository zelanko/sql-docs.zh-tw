---
title: "經由 Proxy 伺服器連線到 SQL Server (SQL Server 組態管理員) | Microsoft Docs"
ms.custom: 
ms.date: 12/15/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Remote WinSock
- RWS
- LATs
- proxy servers [SQL Server]
- connections [SQL Server], proxy server
- Microsoft Proxy Server [SQL Server]
- local address tables [SQL Server]
ms.assetid: 39714de0-2a1f-4179-9091-5c3fa4612545
caps.latest.revision: "22"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c6781cce5ed2b04d72a8eeec9bcba9a5688e3e53
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="connect-to-sql-server-through-a-proxy-server-sql-server-configuration-manager"></a>經由 Proxy 伺服器連接至 SQL Server (SQL Server 組態管理員)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  此主題描述如何使用 SQL Server 組態管理員，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中透過 Proxy 伺服器連接到 SQL Server。 若要使用遠端 WinSock (RWS) 的方法進行遠端接聽，請定義 Proxy Server 的本機位址資料表 (LAT)，使接聽節點位址在 LAT 項目範圍之外。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server 組態管理員  
  
#### <a name="to-enable-connections-to-sql-server-through-microsoft-proxy-server"></a>若要透過 Microsoft Proxy Server 連接到 SQL Server  
  
1.  請遵循[設定伺服器接聽特定 TCP 通訊埠 &#40;SQL Server 組態管理員&#41;](../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md) 中的步驟，來判斷 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 所使用的 TCP/IP 通訊埠為何，或是將 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 設定為使用指定的通訊埠。  
  
2.  在您的 Proxy 伺服器中，定義 Proxy 伺服器的本機位址資料表 (LAT)，使接聽節點位址不在 LAT 項目的範圍內。 如需詳細資訊，請參閱您的 Proxy 伺服器文件集。  
  
>  [!NOTE]
>  本主題適用於內部部署 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。 如需與 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]相關的連線問題，請參閱 [針對 Azure SQL Database 連線問題進行疑難排解](https://docs.microsoft.com/azure/sql-database/sql-database-troubleshoot-common-connection-issues)。  



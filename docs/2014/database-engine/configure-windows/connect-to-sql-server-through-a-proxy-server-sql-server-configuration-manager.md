---
title: 透過 Proxy 伺服器（SQL Server 組態管理員）連接到 SQL Server |Microsoft Docs
ms.custom: ''
ms.date: 06/22/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Remote WinSock
- RWS
- LATs
- proxy servers [SQL Server]
- connections [SQL Server], proxy server
- Microsoft Proxy Server [SQL Server]
- local address tables [SQL Server]
ms.assetid: 39714de0-2a1f-4179-9091-5c3fa4612545
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: de22ad6043c509f08471a6bea40c0efa18d76842
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84935469"
---
# <a name="connect-to-sql-server-through-a-proxy-server-sql-server-configuration-manager"></a>經由 Proxy 伺服器連接至 SQL Server (SQL Server 組態管理員)
  此主題描述如何使用 SQL Server 組態管理員，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中透過 Proxy 伺服器連接到 SQL Server。 若要使用遠端 WinSock (RWS) 的方法進行遠端接聽，請定義 Proxy Server 的本機位址資料表 (LAT)，使接聽節點位址在 LAT 項目範圍之外。  
  
##  <a name="using-sql-server-configuration-manager"></a><a name="SSMSProcedure"></a> 使用 SQL Server 組態管理員  
  
#### <a name="to-enable-connections-to-sql-server-through-microsoft-proxy-server"></a>若要透過 Microsoft Proxy Server 連接到 SQL Server  
  
1.  請遵循[設定伺服器接聽特定 TCP 通訊埠 &#40;SQL Server 組態管理員&#41;](configure-a-server-to-listen-on-a-specific-tcp-port.md) 中的步驟，來判斷 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 所使用的 TCP/IP 通訊埠為何，或是將 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 設定為使用指定的通訊埠。  
  
2.  在您的 Proxy 伺服器中，定義 Proxy 伺服器的本機位址資料表 (LAT)，使接聽節點位址不在 LAT 項目的範圍內。 如需詳細資訊，請參閱您的 Proxy 伺服器文件集。  
  
  

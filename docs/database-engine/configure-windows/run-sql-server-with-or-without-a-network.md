---
title: "使用或不使用網路執行 SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- verifying Server service has been started
- net start [SQL Server]
- command prompt [SQL Server], connections
- SQL Server services, networks
- status information [SQL Server], Server service
- running SQL Server
- networking [SQL Server], SQL Server with or without
- services [SQL Server], networks
- starting Server service
- SQL Server, running
ms.assetid: 54eac961-5c7a-4481-982d-f93a64b5c2f4
caps.latest.revision: "26"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 17f40cdf4abb8ed1877ed0d893af5bc416d6b22c
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="run-sql-server-with-or-without-a-network"></a>使用 (或不使用) 網路執行 SQL Server
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可在網路上執行，也可在不使用網路的情況下執行。  
  
## <a name="running-sql-server-on-a-network"></a>在網路上執行 SQL Server  
 若要讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 能夠透過網路通訊，就必須執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務。 根據預設， [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 會自行啟動內建的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務。 若要查看是否已啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務，可在命令提示字元中輸入：  
  
 **net start**  
  
 若與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 相關的服務已啟動，則會在 **net start** 輸出中出現下列服務：  
  
-   Analysis Services (MSSQLSERVER)  
  
-   SQL Server (MSSQLSERVER)  
  
-   SQL Server Agent (MSSQLSERVER)  
  
## <a name="running-sql-server-without-a-network"></a>不使用網路執行 SQL Server  
 在不使用網路的情況下執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體時，就不需要內建的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務。 即使未使用網路， [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、SQL Server 組態管理員以及 **net start** 和 **net stop** 命令仍可作用，因此啟動及停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的程序，與在網路作業或獨立作業中的程序相同。  
  
 從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sqlcmd **之類的本機用戶端連接獨立的**執行個體時，您可以不使用網路，而使用本機管道直接連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。 本機管道與網路管道的差別在於是否使用網路。 除非另外指向，否則本機與網路管道都會使用標準管道 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .\pipe\sql\query) 建立與\\\\執行個體的連接。  
  
 當您未指定伺服器名稱而連接到本機 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體時，就會使用本機管道。 當您連接到本機 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，並明確指定伺服器名稱時，使用的是網路管道或別的網路跨處理序通訊 (IPC) 機制，如 Internetwork Packet Exchange (IPX) /Sequenced Packet Exchange (SPX) (假設您已將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 設成可使用多個網路)。 由於獨立的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支援網路管道，因此從用戶端連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體時，必須省略不必要的 **/**<伺服器名稱> 引數。 例如，若要從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] osql **連接到獨立**執行個體，請輸入：  
  
 **osql /Usa /P** \<sa 密碼>  
  
  

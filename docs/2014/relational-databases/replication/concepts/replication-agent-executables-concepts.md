---
title: 複寫代理程式可執行檔概念 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
helpviewer_keywords:
- programming interfaces [SQL Server replication]
- programming [SQL Server replication], agents
- replication [SQL Server], agents and profiles
- agents [SQL Server replication], executables
- command prompt [SQL Server replication]
ms.assetid: cba476df-d4ea-44c9-bb86-81488971e328
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 451b7ca4cc06269f116c62be2ef7f01f0e33abd2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62721884"
---
# <a name="replication-agent-executables-concepts"></a>複寫代理程式可執行檔概念
  複寫代理程式可以用下列方式以程式設計方式來控制：  
  
-   在 <xref:Microsoft.SqlServer.Replication> 命名空間中使用 Managed 代理程式來程式設計介面。  
  
-   從命令提示字元以一組提供的參數來叫用代理程式可執行檔。  
  
 從命令提示字元直接叫用複寫代理程式，可讓代理程式從批次檔的命令列指令碼中以程式設計的方式存取。 從命令提示字元叫用代理程式時，它會在叫用代理程式或是啟動批次檔之該使用者的 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 安全性帳戶之下執行。  
  
 下列複寫代理程式的執行個體，可以使用可執行檔來執行。  
  
-   [Replication Distribution Agent](../agents/replication-distribution-agent.md)  
  
-   [複寫記錄讀取器代理程式](../agents/replication-log-reader-agent.md)  
  
-   [Replication Merge Agent](../agents/replication-merge-agent.md)  
  
-   [複寫佇列讀取器代理程式](../agents/replication-queue-reader-agent.md)  
  
-   [Replication Snapshot Agent](../agents/replication-snapshot-agent.md)  
  
 叫用複寫代理程式時，您可以使用效能設定檔，將一組定義的參數自動傳遞到代理程式可執行檔。 如需相關資訊，請參閱 [Replication Agent Profiles](../agents/replication-agent-profiles.md)。  
  
## <a name="examples"></a>範例  
 下列範例顯示如何從命令提示字元叫用複寫代理程式。 複寫代理程式也可以透過 Replication Management Objects (RMO) 來叫用。 如需詳細資訊，請參閱[同步處理訂閱 &#40;複寫&#41;](../synchronize-data.md)。  
  
> [!NOTE]  
>  在這些範例中加入了分行符號，以提升可讀性。 在批次檔中，必須在單一行中撰寫命令。  
  
### <a name="running-the-snapshot-agent"></a>執行快照集代理程式。  
 這個範例批次檔會從命令提示字元叫用「快照集代理程式」，以產生 **AdvWorksSalesOrdersMerge** 發行集的快照集  
  
```  
REM -- Declare variables  
SET Publisher=%InstanceName%;  
SET PublicationDB=AdventureWorks2012;   
SET Publication=AdvWorksSalesOrdersMerge;   
  
REM --Start the Snapshot Agent to generate the snapshot for AdvWorksSalesOrdersMerge.  
"C:\Program Files\Microsoft SQL Server\120\COM\SNAPSHOT.EXE" -Publication %Publication%   
-Publisher %Publisher% -Distributor %Publisher% -PublisherDB %PublicationDB%   
-ReplicationType 2 -OutputVerboseLevel 1 -DistributorSecurityMode 1 ;  
  
```  
  
### <a name="running-the-distribution-agent"></a>執行散發代理程式。  
 這個範例批次檔會從命令提示字元叫用「散發代理程式」，以繼續從 **AdvWorksProductTran** 發行集將變更複寫到發送訂閱者。  
  
```  
REM -- Declare the variables.  
SET Publisher=%instancename%;  
SET Subscriber=%instancename%;  
SET PublicationDB=AdventureWorks2012;  
SET SubscriptionDB=AdventureWorks2012Replica;   
SET Publication=AdvWorksProductsTran;  
  
REM -- Start the Distribution Agent with four subscription streams.  
REM -- The following command must be supplied without line breaks.  
"C:\Program Files\Microsoft SQL Server\120\COM\DISTRIB.EXE" -Subscriber %Subscriber%   
-SubscriberDB %SubscriptionDB% -SubscriberSecurityMode 1 -Publication %Publication%   
-Publisher %Publisher% -PublisherDB %PublicationDB% -Distributor %Publisher%   
-DistributorSecurityMode 1 -Continuous -SubscriptionType 0 -SubscriptionStreams 4 ;  
  
```  
  
### <a name="running-the-merge-agent"></a>執行合併代理程式  
 這個範例批次檔會從命令提示字元叫用「合併代理程式」，以將提取訂閱同步處理到 **AdvWorksSalesOrdersMerge** 發行集。  
  
```  
REM -- Declare the variables.  
SET Publisher=%instancename%;  
SET Subscriber=%instancename%;  
SET PublicationDB=AdventureWorks2012;  
SET SubscriptionDB=AdventureWorks2012Replica;   
SET Publication=AdvWorksSalesOrdersMerge;  
  
REM --Start the Merge Agent with concurrent upload and download processes.  
REM -- The following command must be supplied without line breaks.  
"C:\Program Files\Microsoft SQL Server\120\COM\REPLMERG.EXE" -Publication %Publication%    
-Publisher %Publisher%  -Subscriber  %Subscriber%  -Distributor %Publisher%    
-PublisherDB %PublicationDB%  -SubscriberDB %SubscriptionDB% -PublisherSecurityMode 1    
-OutputVerboseLevel 2  -SubscriberSecurityMode 1  -SubscriptionType 1 -DistributorSecurityMode 1    
-Validate 3  -ParallelUploadDownload 1 ;  
  
```  
  
  

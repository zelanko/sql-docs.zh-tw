---
title: 複寫代理程式概觀 | Microsoft Docs
description: 了解代理程式，SQL Server 複寫使用其來執行與追蹤變更及散發資料建立關聯的工作。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Distribution Agent
- agents [SQL Server replication]
- Queue Reader Agent, about Queue Reader Agent
- Queue Reader Agent
- Merge Agent, about Merge Agent
- Log Reader Agent, about Log Reader Agent
- replication [SQL Server], agents and profiles
- Log Reader Agent
- Distribution Agent, about Distribution Agent
- agents [SQL Server replication], about agents
- Merge Agent
- Snapshot Agent, about Snapshot Agent
- Snapshot Agent
ms.assetid: a35ecd7d-f130-483c-87e3-ddc8927bb91b
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 18b3914f2ed9be429f29b929bc74623af9f707bf
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86922836"
---
# <a name="replication-agents-overview"></a>複寫代理程式概觀
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]
  複寫使用了許多名為代理程式的獨立程式，以執行與追蹤變更和散發資料有關的工作。 依預設，複寫代理程式作為在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 中排定的作業來執行，且必須執行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 方可執行這些作業。 複寫代理程式也可以從命令列執行，或透過使用 Replication Management Objects (RMO) 的應用程式執行。 複寫代理程式可以透過「 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 複寫監視器」和 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]進行管理。  
  
## <a name="sql-server-agent"></a>SQL Server Agent  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 主控和排程複寫中使用的代理程式，並為執行複寫代理程式提供了簡易的方法。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 還控制和監視除複寫以外的其他作業。 如需詳細資訊，請參閱 [Configure SQL Server Agent](../../../ssms/agent/configure-sql-server-agent.md)。  
  
> [!IMPORTANT]  
>  依預設，安裝 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 時會停用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 服務，除非明確選擇在安裝期間自動啟動該服務。 如需有關啟動 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 服務的詳細資訊，請參閱＜ [Start, Stop, or Pause the SQL Server Agent Service](https://msdn.microsoft.com/library/c95a9759-dd30-4ab6-9ab0-087bb3bfb97c)進行管理。  
  
## <a name="snapshot-agent"></a>快照集代理程式  
 「快照集代理程式」通常搭配各種類型的複寫使用， 它會準備已發行資料表和其他物件的結構描述和初始資料檔、儲存快照集檔案，並記錄散發資料庫中同步處理的相關資訊。 快照集代理程式於發行者端執行。 如需詳細資訊，請參閱 [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)。  
  
## <a name="log-reader-agent"></a>記錄讀取器代理程式  
 「記錄讀取器代理程式」(Log Reader Agent) 可搭配異動複寫來使用。 它可將標示為複寫的交易，自「發行者」的交易記錄移至散發資料庫中。 每個使用異動複寫發行的資料庫都擁有其自己的「記錄讀取器代理程式」，該代理程式在「散發者」端執行並連接到「發行者」(「散發者」可與「發行者」在同一台電腦)。 如需詳細資訊，請參閱 [Replication Log Reader Agent](../../../relational-databases/replication/agents/replication-log-reader-agent.md)。  
  
## <a name="distribution-agent"></a>散發代理程式  
 「散發代理程式」(Distribution Agent) 可搭配快照式複寫和異動複寫來使用。 它可將初始快照集套用至「訂閱者」，並將散發資料庫中的交易移至「訂閱者」。 「散發代理程式」在發送訂閱的「散發者」端或是提取訂閱的「訂閱者」端執行。 如需詳細資訊，請參閱 [Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)。  
  
## <a name="merge-agent"></a>合併代理程式  
 「合併代理程式」(Merge Agent) 可搭配合併式複寫使用。 它可將初始快照集套用到「訂閱者」，移動並使累加的資料變更一致。 每個合併訂閱都有其「合併代理程式」，以連接「發行者」和「訂閱者」，並更新這兩者。 「合併代理程式」在發送訂閱的「散發者」端或是提取訂閱的「訂閱者」端執行。 依預設，「合併代理程式」將變更從「訂閱者」上傳到「發行者」，然後再將變更從「發行者」下載至「訂閱者」。 如需詳細資訊，請參閱 [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)。  
  
## <a name="queue-reader-agent"></a>佇列讀取器代理程式  
 「佇列讀取器代理程式」與具有佇列更新選項的異動複寫搭配使用。 代理程式在「散發者」端執行，並且將在「訂閱者」端所作的變更移回至「發行者」。 它不像「散發代理程式」和「合併代理程式」，只存在一個「佇列讀取器代理程式」的執行個體，來服務所有的「發行者」和指定散發資料庫的發行集。 如需「佇列讀取器代理程式」的詳細資訊，請參閱＜ [Replication Queue Reader Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)＞。 如需有關可更新訂閱的詳細資訊，請參閱＜ [Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)＞。  
  
## <a name="replication-maintenance-jobs"></a>複寫維護作業  
 複寫擁有許多依排程和視需要執行維護的維護作業。 如需詳細資訊，請參閱[複寫代理程式管理](../../../relational-databases/replication/agents/replication-agent-administration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [啟動及停止複寫代理程式 &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)   
 [執行複寫維護作業 &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/administration/run-replication-maintenance-jobs-sql-server-management-studio.md)   
 [複寫代理程式可執行檔概念](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)   
 [複寫代理程式管理](../../../relational-databases/replication/agents/replication-agent-administration.md)  
  
  

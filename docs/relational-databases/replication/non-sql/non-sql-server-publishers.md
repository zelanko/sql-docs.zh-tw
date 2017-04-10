---
title: "非 SQL Server 發行者 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "異質資料庫複寫，非 SQL Server 發行者"
  - "非 SQL Server 發行者"
  - "異質資料來源，非 SQL Server 發行者"
  - "發行者 [SQL Server 複寫]，Oracle"
ms.assetid: 08a160a6-33be-46b5-bc7b-d53180d8bdf1
caps.latest.revision: 31
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 31
---
# 非 SQL Server 發行者
  將資料從非發行[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 來源可讓您合併資料 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可訂閱從 Oracle 資料庫發行的快照或交易資料。 如需從 Oracle 發行的詳細資訊，請參閱 [Oracle 發行概觀](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)。  
  
 非 SQL Server 訂閱者的異質性複寫已被取代。 Oracle 發行已被取代。 若要移動資料，請使用異動資料擷取和 [!INCLUDE[ssIS](../../../includes/ssis-md.md)]建立方案。  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 從非 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫發行對於下列狀況來說相當理想︰  
  
|狀況|描述|  
|--------------|-----------------|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 應用程式部署|使用 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio 和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 進行開發，同時操作從非 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫複寫的資料。|  
|資料倉儲臨時伺服器|保留 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 臨時資料庫同步處理與非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫。|  
|移轉至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|在複寫來源系統的變更時，即時針對 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 測試您的應用程式。 完成移轉時切換至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。|  
  
## 另請參閱  
 [異質資料庫複寫](../../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)  
  
  
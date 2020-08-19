---
description: 非 SQL Server 發行者
title: 非 SQL Server 發行者 | Microsoft Docs
ms.custom: ''
ms.date: 08/29/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- heterogeneous database replication, non-SQL Server Publishers
- non-SQL Server Publishers
- heterogeneous data sources, non-SQL Server Publishers
- Publishers [SQL Server replication], Oracle
ms.assetid: 08a160a6-33be-46b5-bc7b-d53180d8bdf1
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9560875e4db3a644644238b0140fadb33cf1877d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88420442"
---
# <a name="non-sql-server-publishers"></a>非 SQL Server 發行者  
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

從非 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 來源發行資料，可讓您合併 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的資料。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可訂閱從 Oracle 資料庫發行的快照或交易資料。 如需從 Oracle 發行的詳細資訊，請參閱 [Oracle 發行概觀](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)。  
  
[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 支援下列交易式與快照式複寫的異質性情況：  
  
-   將資料從 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 發行到非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的訂閱者  

-   在 Oracle 之間發行資料的限制如下：  

  |複寫 |2016 或更早版本 |2017 或更新版本 |
  |:-----------|:---------------|:-------------|
  |從 Oracle 複寫 |只支援 Oracle 10g 或更早版本 |只支援 Oracle 10g 或更早版本 |
  |複寫到 Oracle |最高到 Oracle 12c |不支援 |
  | &nbsp; | &nbsp; | &nbsp; |


 非 SQL Server 訂閱者的異質性複寫已被取代。 Oracle 發行已被取代。 若要移動資料，請使用異動資料擷取和 [!INCLUDE[ssIS](../../../includes/ssis-md.md)]建立方案。  
  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 從非 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫發佈對於下列狀況來說相當理想：  
  
|案例|描述|  
|--------------|-----------------|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 應用程式部署|使用 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio 和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 進行開發，同時操作從非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫複寫的資料。|  
|資料倉儲臨時伺服器|保持 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 臨時資料庫與非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫的同步處理。|  
|移轉至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|在複寫來源系統的變更時，即時針對 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 測試您的應用程式。 完成移轉時切換至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。|  
  
## <a name="see-also"></a>另請參閱  
 [異質資料庫複寫](../../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)  
  
  

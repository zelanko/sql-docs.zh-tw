---
title: 非 SQL Server 發行者 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- heterogeneous database replication, non-SQL Server Publishers
- non-SQL Server Publishers
- heterogeneous data sources, non-SQL Server Publishers
- Publishers [SQL Server replication], Oracle
ms.assetid: 08a160a6-33be-46b5-bc7b-d53180d8bdf1
caps.latest.revision: 30
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fbb2694932b20c38bee4bc7b3978abfab1472b43
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37299908"
---
# <a name="non-sql-server-publishers"></a>非 SQL Server 發行者
  從非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 來源發行資料，可讓您合併 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中的資料。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可訂閱從 Oracle 資料庫發行的快照或交易資料。 如需從 Oracle 發行的詳細資訊，請參閱 [Oracle 發行概觀](oracle-publishing-overview.md)。  
  
 非 SQL Server 訂閱者的異質性複寫已被取代。 Oracle 發行已被取代。 若要移動資料，請使用異動資料擷取和 [!INCLUDE[ssIS](../../../includes/ssis-md.md)]建立方案。  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 從非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫發行對於下列狀況來說相當理想︰  
  
|狀況|描述|  
|--------------|-----------------|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 應用程式部署|使用 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio 和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 進行開發，同時操作從非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫複寫的資料。|  
|資料倉儲臨時伺服器|保持 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 臨時資料庫與非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫的同步處理。|  
|移轉至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|在複寫來源系統的變更時，即時針對 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 測試您的應用程式。 完成移轉時切換至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。|  
  
## <a name="see-also"></a>另請參閱  
 [Heterogeneous Database Replication](heterogeneous-database-replication.md)  
  
  

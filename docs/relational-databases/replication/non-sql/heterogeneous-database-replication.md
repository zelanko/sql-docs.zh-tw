---
title: 異質資料庫複寫 | Microsoft Docs
ms.custom: ''
ms.date: 08/28/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- heterogeneous database replication, about heterogeneous database replication
- replication [SQL Server], heterogeneous database replication
- heterogeneous database replication
ms.assetid: 3fd983ad-e206-45db-9054-417c9b5bb815
caps.latest.revision: 41
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 77bf8eb00bdc54901e3b84250319212f1eac22a0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32962543"
---
# <a name="heterogeneous-database-replication"></a>異質資料庫複寫  
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 支援下列交易式與快照式複寫的異質性情況：  
  
-   將資料從 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 發行到非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的訂閱者  

-   在 Oracle 之間發行資料的限制如下：  
  | |2016 或更早版本 |2017 或更新版本 |
  |-------|-------|--------|
  |從 Oracle 複寫 |只支援 Oracle 10g 或更早版本 |只支援 Oracle 10g 或更早版本 |
  |複寫到 Oracle |最高到 Oracle 12c |不支援 |


 非 SQL Server 訂閱者的異質性複寫已被取代。 Oracle 發行已被取代。 若要移動資料，請使用異動資料擷取和 [!INCLUDE[ssIS](../../../includes/ssis-md.md)]建立方案。  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
## <a name="publishing-data-from-oracle"></a>從 Oracle 發行資料  
 您可以使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 從大部份功能及易用性皆與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 快照式和異動複寫相同的 Oracle 中發行資料。 這項功能需要 Oracle 10g 或更早版本。 下列狀況適合從 Oracle 發行資料：  
  
|狀況|描述|  
|--------------|-----------------|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 應用程式部署|使用 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio 和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 進行開發，同時操作從非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫複寫的資料。|  
|資料倉儲臨時伺服器|保持 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 臨時資料庫與非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫的同步處理。|  
|移轉至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|在複寫來源系統的變更時，即時針對 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 測試您的應用程式。 完成移轉時切換至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。|  
  
 如需詳細資訊，請參閱 [Oracle 發行概觀](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)。  
  
## <a name="publishing-data-to-non-sql-server-subscribers"></a>將資料發行至非 SQL Server 訂閱者  
 下列非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫做為快照式和交易式發行集的「訂閱者」得到支援：  
  
-   Oracle 支援之所有平台的 Oracle。  
  
-   IBM DB2 (適用於 AS400、MVS、Unix、Linux 和 Windows)。  
  
 如需詳細資訊，請參閱 [Non-SQL Server Subscribers](../../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)。  
  
  

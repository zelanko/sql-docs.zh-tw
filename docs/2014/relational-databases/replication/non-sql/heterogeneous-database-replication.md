---
title: 異質資料庫複寫 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- heterogeneous database replication, about heterogeneous database replication
- replication [SQL Server], heterogeneous database replication
- heterogeneous database replication
ms.assetid: 3fd983ad-e206-45db-9054-417c9b5bb815
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 543fd750047d171e353940bc2b4a22a4e54aed57
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63022467"
---
# <a name="heterogeneous-database-replication"></a>異質資料庫複寫
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 支援下列交易式與快照式複寫的異質性情況：  
  
-   將資料從 Oracle 發行到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
-   將資料從 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 發行到非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的訂閱者  
  
 非 SQL Server 訂閱者的異質性複寫已被取代。 Oracle 發行已被取代。 若要移動資料，請使用異動資料擷取和 [!INCLUDE[ssIS](../../../includes/ssis-md.md)]建立方案。  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
## <a name="publishing-data-from-oracle"></a>從 Oracle 發行資料  
 您可以使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 從大部份功能及易用性皆與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 快照式和異動複寫相同的 Oracle 中發行資料。 下列狀況適合從 Oracle 發行資料：  
  
|狀況|描述|  
|--------------|-----------------|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 應用程式部署|使用 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio 和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 進行開發，同時操作從非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫複寫的資料。|  
|資料倉儲臨時伺服器|保持 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 臨時資料庫與非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫的同步處理。|  
|移轉至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|在複寫來源系統的變更時，即時針對 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 測試您的應用程式。 完成移轉時切換至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。|  
  
 如需詳細資訊，請參閱 [Oracle 發行概觀](oracle-publishing-overview.md)。  
  
## <a name="publishing-data-to-non-sql-server-subscribers"></a>將資料發行至非 SQL Server 訂閱者  
 下列非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫做為快照式和交易式發行集的「訂閱者」得到支援：  
  
-   Oracle 支援之所有平台的 Oracle。  
  
-   IBM DB2 (適用於 AS400、MVS、Unix、Linux 和 Windows)。  
  
 如需詳細資訊，請參閱 [Non-SQL Server Subscribers](non-sql-server-subscribers.md)。  
  
  

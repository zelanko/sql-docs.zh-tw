---
title: Oracle 發行概觀 | Microsoft Docs
ms.custom: ''
ms.date: 08/29/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- publishing [SQL Server replication], Oracle publishing
- snapshot replication [SQL Server], Oracle publishing
- Oracle publishing [SQL Server replication]
- transactional replication, Oracle publishing
- Oracle publishing [SQL Server replication], about Oracle publishing
ms.assetid: 2e013259-0022-4897-a08d-5f8deb880fa8
caps.latest.revision: 40
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: dd1e46d3637b039a4e261dc78e21ed0d954ee2b9
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37350390"
---
# <a name="oracle-publishing-overview"></a>Oracle Publishing Overview  
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

從 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]開始，您可以將 Oracle 發行者包含在複寫拓撲中 (從 Oracle 9i 版開始)。 發行伺服器可以部署在任何 Oracle 支援的硬體和作業系統上。 此功能是建立在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 快照式複寫與異動複寫的堅實基礎上，可以提供相近的效能與可用性。  
  
[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 支援下列交易式與快照式複寫的異質性情況：  
  
-   將資料從 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 發行到非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的訂閱者  

-   在 Oracle 之間發行資料的限制如下：  
  | |2016 或更早版本 |2017 或更新版本 |
  |-------|-------|--------|
  |從 Oracle 複寫 |只支援 Oracle 10g 或更早版本 |只支援 Oracle 10g 或更早版本 |
  |複寫到 Oracle |最高到 Oracle 12c |不支援 |


 非 SQL Server 訂閱者的異質性複寫已被取代。 Oracle 發行已被取代。 若要移動資料，請使用異動資料擷取和 [!INCLUDE[ssIS](../../../includes/ssis-md.md)]建立方案。  

  
## <a name="snapshot-replication-for-oracle"></a>Oracle 的快照式複寫  
 實作 Oracle 快照式發行集的方法與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 快照式發行集相似。 針對 Oracle 發行集執行快照集代理程式時，代理程式會連接到 Oracle 發行者，並處理複寫中的每個資料表。 代理程式在處理每個資料表時，會擷取資料表資料列並建立結構描述指令碼，然後儲存在發行集的快照集共用裡。 快照集代理程式每次執行時都會建立整組資料，所以變更追蹤觸發程序不會像使用異動複寫時一樣加入 Oracle 資料表。 快照式複寫提供一個便利的方式，能在對發行系統影響最小的情形下移轉資料。  
  
## <a name="transactional-replication-for-oracle"></a>Oracle 的異動複寫  
 Oracle 異動複寫是使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的異動複寫架構實作；不過，是使用 Oracle 資料庫與記錄讀取器代理程式上的資料庫觸發程序組合來追蹤變更。 Oracle 異動複寫的訂閱者會使用快照式複寫自動初始化；發生後續變更時，會透過記錄讀取器代理程式追蹤並傳遞至訂閱者。  
  
 建立 Oracle 發行集時，會為 Oracle 資料庫中每一個發行資料表建立觸發程序與追蹤資料表。 變更發行資料表中的資料時，資料表上的資料庫觸發程序會引發，並將資訊插入每個已修改之資料列的複寫追蹤資料表。 然後 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 散發者上的記錄讀取器代理程式會將資料變更資訊從追蹤資料表移至散發者上的散發資料庫。 最後，如同標準異動複寫一樣，散發代理程式會將變更從散發者移至訂閱者。  
  
## <a name="see-also"></a>另請參閱  
 [設定 Oracle 發行者](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Oracle 發行相關術語字彙](../../../relational-databases/replication/non-sql/glossary-of-terms-for-oracle-publishing.md)   
 [異質資料庫複寫](../../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)  
  
  

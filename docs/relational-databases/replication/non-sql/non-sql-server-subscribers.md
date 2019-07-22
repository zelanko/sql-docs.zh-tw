---
title: 非 SQL Server 訂閱者 | Microsoft Docs
ms.custom: ''
ms.date: 08/29/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [SQL Server replication], non-SQL Server Subscribers
- heterogeneous data sources, non-SQL Server Subscribers
- heterogeneous data sources
- heterogeneous database replication, non-SQL Server Subscribers
- non-SQL Server Subscribers, about non-SQL Server Subscribers
- heterogeneous Subscribers
- heterogeneous Subscribers, about heterogeneous Subscribers
- Subscribers [SQL Server replication], non-SQL Server Subscribers
- non-SQL Server Subscribers
ms.assetid: 831e7586-2949-4b9b-a2f3-7b0b699b23ff
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 26bda5e190f18469948f935302ee2cbf9ddd121c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67940408"
---
# <a name="non-sql-server-subscribers"></a>非 SQL Server 訂閱者  
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

下列非「[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 訂閱者」可以使用發送訂閱來訂閱快照式和交易式發行集。 使用已列 OLE DB 提供者的最新版本，列出的每個資料庫之兩個最新版本可支援訂閱。  
  
 非 SQL Server 訂閱者的異質性複寫已被取代。 Oracle 發行已被取代。 若要移動資料，請使用異動資料擷取和 [!INCLUDE[ssIS](../../../includes/ssis-md.md)]建立方案。  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
|[資料庫]|作業系統|提供者|  
|--------------|----------------------|--------------|  
|Oracle|Oracle 支援的所有平台|Oracle OLE DB 提供者 (由 Oracle 提供)|  
|IBM DB2|MVS、AS400、Unix、Linux 與 Windows (不包括 9.x)|Microsoft Host Integration Server (HIS) OLE DB 提供者|  

Oracle 版本資訊：  
[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 支援下列交易式與快照式複寫的異質性情況：  
  
-   將資料從 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 發行到非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的訂閱者  

-   在 Oracle 之間發行資料的限制如下：  

  | 複寫|2016 或更早版本 |2017 或更新版本 |
  |:-----------|:---------------|:-------------|
  |從 Oracle 複寫 |只支援 Oracle 10g 或更早版本 |只支援 Oracle 10g 或更早版本 |
  |複寫到 Oracle |最高到 Oracle 12c |不支援 |
  | &nbsp; | &nbsp; | &nbsp; |


 非 SQL Server 訂閱者的異質性複寫已被取代。 Oracle 發行已被取代。 若要移動資料，請使用異動資料擷取和 [!INCLUDE[ssIS](../../../includes/ssis-md.md)]建立方案。  

如需建立 Oracle 和 IBM DB2, 之訂閱的詳細資訊，請參閱＜ [Oracle 訂閱者](../../../relational-databases/replication/non-sql/oracle-subscribers.md) ＞和＜ [IBM DB2 Subscribers](../../../relational-databases/replication/non-sql/ibm-db2-subscribers.md)建立方案。  
  
## <a name="considerations-for-non-sql-server-subscribers"></a>非 SQL Server 訂閱者之考量  
 當複寫到非「[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 訂閱者」時，請記住下列考量：  
  
### <a name="general-considerations"></a>一般考量  
  
-   複寫支援將資料表和索引檢視做為資料表發行至非「[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 訂閱者」(索引檢視無法複寫為索引檢視)。  
  
-   在「新增發行集精靈」中建立發行集，然後使用 [發行集屬性] 對話方塊為非「SQL Server 訂閱者」啟用此發行集時，不會為非「[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 訂閱者」指定訂閱資料庫中所有物件的擁有者，而對於「 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 訂閱者」，會設為發行集資料庫中對應物件的擁有者。  
  
-   如果發行集擁有「[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 訂閱者」和「非 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 訂閱者」，則必須先為「非 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 訂閱者」啟用發行集，之後再建立「[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 訂閱者」的任何訂閱。  
  
-   根據預設，由「快照集代理程式」為「非 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 訂閱者」產生的指令碼會在 `CREATE TABLE` 語法中使用未加引號的識別碼。 因此，名稱為 test 的已發行資料表會複寫為 TEST。 若要使用與發行集資料庫中資料表相同的大小寫，請使用「散發代理程式」的 **-QuotedIdentifier** 參數。 如果發行的物件名稱 (如資料表、資料行或條件約束) 包含空格或非「 **訂閱者」端之資料庫版本中的保留字，則還必須使用** -QuotedIdentifier[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 參數。 如需有關此參數的詳細資訊，請參閱＜ [Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)＞。  
  
-   「散發代理程式」執行時所用的帳戶必須具有 OLE DB 提供者安裝目錄的讀取權限。  
  
-   依預設，對於非「[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 訂閱者」，「散發代理程式」為訂閱資料庫 (「散發代理程式」的 **-SubscriberDB** 參數) 使用 [(預設目的地)] 的值：  
  
    -   在 Oracle 中，伺服器最多只有一個資料庫，所以不需要指定資料庫。  
  
    -   對於 IBM DB2，在 DB2 連接字串中指定資料庫。 如需相關資訊，請參閱 [為非 SQL Server 訂閱者建立訂閱](../../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md)。  
  
-   如果「[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 散發者」是在 64 位元平台上執行，則必須使用適當的 64 位元版本 OLE DB 提供者。  
  
-   複寫以 Unicode 格式移動資料，不論「發行者」與「訂閱者」上使用的定序/字碼頁為何。 在「發行者」和「訂閱者」之間複寫時，建議您選擇相容的定序/字碼頁。  
  
-   如果在發行集中新增或刪除發行項，則必須重新初始化非「[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 訂閱者」的訂閱。  
  
-   所有非「[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 訂閱者」支援的條件約束僅為：NULL 和 NOT NULL。 主索引鍵條件約束複寫為唯一的索引。  
  
-   不同資料庫以不同方式處理值 NULL，這會影響空白值、空字串和 NULL 的表示方式。 進而會影響插入到定義了唯一條件約束的資料行之值的行為。 例如，Oracle 在視為唯一的資料行中允許有多個 NULL 值，而 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 在唯一的資料行中只允許有一個 NULL 值。  
  
     另一個因素是，當資料行定義為 NOT NULL 時，如何處理 NULL 值、空字串和空白值。 如需為「Oracle 訂閱者」解決此問題的詳細資訊，請參閱＜ [Oracle Subscribers](../../../relational-databases/replication/non-sql/oracle-subscribers.md)＞。  
  
-   移除訂閱時，與複寫相關的中繼資料 (交易序號資料表) 不會從非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 訂閱者刪除。  
  
### <a name="conforming-to-the-requirements-of-the-subscriber-database"></a>符合訂閱者資料庫之要求  
  
-   發行的結構描述和資料必須符合「訂閱者」端資料庫的要求。 例如，如果非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫的最大資料列大小小於 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，則必須確定已發行的結構描述和資料不會超過此大小。  
  
-   複寫到非「[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 訂閱者」的資料表將採用「訂閱者」端資料庫的資料表命名慣例。  
  
-   非 SQL Server 訂閱者不支援 DDL。 如需結構描述變更的詳細資訊，請參閱[對發行集資料庫進行結構描述變更](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)。  
  
### <a name="replication-feature-support"></a>複寫功能支援  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 提供兩種訂閱類型：發送訂閱和提取訂閱。 非「[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 訂閱者」必須使用發送訂閱，該訂閱中「散發代理程式」在「 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 散發者」端執行。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 提供兩種快照集格式：原生 bcp 模式以及字元模式。 非「[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 訂閱者」需要字元模式快照集。  
  
-   非「[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 訂閱者」不能使用立即更新或佇列更新訂閱，或成為點對點拓撲中的節點。  
  
-   非「[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 訂閱者」不能從備份中自動初始化。  
  
## <a name="see-also"></a>另請參閱  
 [異質資料庫複寫](../../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [訂閱發行集](../../../relational-databases/replication/subscribe-to-publications.md)  
  
  

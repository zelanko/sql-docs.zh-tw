---
title: 管理變更追蹤 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: track-changes
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- tracking data changes [SQL Server]
- change tracking [SQL Server], overhead
- change tracking [SQL Server]
- change tracking [SQL Server], managing
ms.assetid: 94a8d361-e897-4d6d-9a8f-1bb652e7a850
caps.latest.revision: 9
author: rothja
ms.author: jroth
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: b41e499cbc4594526b4540af7825148307aa44bb
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2018
ms.locfileid: "39533608"
---
# <a name="manage-change-tracking-sql-server"></a>管理變更追蹤 (SQL Server)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  本主題描述如何管理變更追蹤。 此外，本主題也會描述如何設定安全性，以及判斷使用變更追蹤對儲存和效能產生的影響。  
  
## <a name="managing-change-tracking"></a>管理變更追縱  
 下列各節將列出與管理變更追蹤有關的目錄檢視、權限和設定。  
  
### <a name="catalog-views"></a>目錄檢視  
 若要判斷哪些資料表和資料庫已啟用變更追蹤，您可以使用下列目錄檢視：  
  
-   [sys.change_tracking_databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/change-tracking-catalog-views-sys-change-tracking-databases.md)  
  
-   [sys.change_tracking_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/change-tracking-catalog-views-sys-change-tracking-tables.md)  
  
 此外，當針對使用者資料表啟用變更追蹤時， [sys.internal_tables](../../relational-databases/system-catalog-views/sys-internal-tables-transact-sql.md) 目錄檢視也會列出所建立的內部資料表。  
  
### <a name="security"></a>Security  
 若要使用 [變更追蹤函數](../../relational-databases/system-functions/change-tracking-functions-transact-sql.md)來存取變更追蹤資訊，主體必須具有以下權限：  
  
-   在所查詢的資料表上，變更追蹤資料表上至少具有主索引鍵資料行的 SELECT 權限。  
  
-   要取得變更之資料表上的 VIEW CHANGE TRACKING 權限。 需要 VIEW CHANGE TRACKING 權限的原因如下：  
  
    -   變更追蹤記錄包含已刪除之資料列的相關資訊，特別是已刪除之資料列的主索引鍵值。 在刪除某些敏感性資料之後，主體可能已經被授與變更追蹤資料表的 SELECT 權限。 在此情況下，您不想讓該主體能夠使用變更追蹤來存取已刪除的資訊。  
  
    -   變更追蹤資訊可儲存有關更新作業已變更哪些資料行的資訊。 當資料行包含敏感性資訊時，可能會拒絕主體對此資料行的存取權限。 不過，由於可使用變更追蹤資訊，所以主體可以判斷資料行值已經更新，但是主體無法判斷此資料行的值。  
  
## <a name="understanding-change-tracking-overhead"></a>了解變更追蹤負擔  
 在針對資料表啟用變更追蹤時，某些管理作業會受到影響。 下表將列出這些作業以及您應該考量的影響。  
  
|作業|啟用變更追蹤時|  
|---------------|-------------------------------------|  
|DROP TABLE|針對卸除的資料表移除了所有變更追蹤資訊。|  
|ALTER TABLE DROP CONSTRAINT|嘗試卸除 PRIMARY KEY 條件約束但卻失敗。 在可以卸除 PRIMARY KEY 條件約束之前，必須先停用變更追蹤。|  
|ALTER TABLE DROP COLUMN|如果所卸除的資料行屬於主索引鍵的一部分，則不允許卸除此資料行 (與變更追蹤無關)。<br /><br /> 如果所卸除的資料行不屬於主索引鍵的一部分，則卸除此資料行將會成功。 但是，應該要先了解對同步處理此資料之任何應用程式的影響。 如果已針對資料表啟用資料行變更追蹤，則仍然可能在變更追蹤資訊中傳回卸除的資料行。 應用程式必須負責處理卸除的資料行。|  
|ALTER TABLE ADD COLUMN|如果新的資料行加入至變更追蹤資料表，系統不會追蹤資料行的加入作業。 系統只會追蹤對新資料行所做的更新和變更。|  
|ALTER TABLE ALTER COLUMN|不會追蹤非主索引鍵資料行的資料類型變更。|  
|ALTER TABLE SWITCH|如果其中一個或兩個資料表已啟用變更追蹤，則切換資料分割會失敗。|  
|DROP INDEX 或 ALTER INDEX DISABLE|強制主索引鍵的索引無法加以卸除或停用。|  
|TRUNCATE TABLE|截斷資料表的作業可以在已啟用變更追蹤的資料表上執行。 但是，不會追蹤此作業所刪除的資料列，而且會更新最小的有效版本。 當應用程式檢查它的版本時，這項檢查會指示此版本太舊，而且需要重新初始化。 這與針對資料表停用變更追蹤然後重新啟用相同。|  
  
 使用變更追蹤並不會對 DML 作業造成額外負擔，因為變更追蹤資訊會儲存成作業的一部分。  
  
### <a name="effects-on-dml"></a>對 DML 的影響  
 變更追蹤已經最佳化，可讓 DML 作業的效能負擔降到最低。 與在資料表上使用變更追蹤有關的累加效能負擔，類似於針對資料表建立索引而且需要進行維護時所產生的負擔。  
  
 對於 DML 作業變更的每一個資料列而言，會將一個資料列新增到內部變更追蹤資料表。 這項作業 (相對於 DML 作業) 的影響取決於各種因素，如下列所示：  
  
-   主索引鍵資料行的數目  
  
-   在使用者資料表資料列中變更的資料數量  
  
-   在交易中執行的作業數目  
  
 如果您使用了快照隔離，它也會影響所有 DML 作業的效能 (不論是否啟用變更追蹤)。  
  
### <a name="effects-on-storage"></a>對儲存的影響  
 變更追蹤資料會儲存在下列內部資料表類型中：  
  
-   內部變更資料表  
  
     啟用變更追蹤的每個使用者資料表都會有一個內部變更資料表。  
  
-   內部交易資料表  
  
     每個資料庫都有一個內部交易資料表。  
  
 這些內部資料表會以下列方式來影響儲存需求：  
  
-   對於使用者資料表內每一個資料列的每一項變更而言，會將一個資料列新增到內部變更資料表。 這個資料列有少量固定的負擔，再加上等於主索引鍵資料行大小的變動負擔。 此資料列可以包含應用程式所設定的選擇性內容資訊。 此外，如果啟用了資料行追蹤，則每一個變更的資料行在追蹤資料表內都需要 4 個位元組。  
  
-   針對每個認可的交易，內部交易資料表都會加入一個資料列。  
  
 如果是其他內部資料表，您可以使用 [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md) 預存程序來判斷用於變更追蹤資料表的空間。 您可以使用 [sys.internal_tables](../../relational-databases/system-catalog-views/sys-internal-tables-transact-sql.md) 目錄檢視來取得內部資料表的名稱，如下列範例所示。  
  
```sql  
sp_spaceused 'sys.change_tracking_309576141'  
sp_spaceused 'sys.syscommittab'  
```  
  
## <a name="see-also"></a>另請參閱  
 [追蹤資料變更 &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [資料庫屬性 &#40;變更追蹤頁面&#41;](../../relational-databases/databases/database-properties-changetracking-page.md)   
 [ALTER DATABASE SET 選項 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [sys.change_tracking_databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/change-tracking-catalog-views-sys-change-tracking-databases.md)   
 [sys.change_tracking_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/change-tracking-catalog-views-sys-change-tracking-tables.md)   
 [追蹤資料變更 &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)   
 [關於變更追蹤 &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-tracking-sql-server.md)   
 [使用變更資料 &#40;SQL Server&#41;](../../relational-databases/track-changes/work-with-change-data-sql-server.md)  
  
  

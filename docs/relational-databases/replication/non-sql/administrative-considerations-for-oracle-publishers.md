---
title: "Oracle 發行者的管理考量 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Oracle 發行 [SQL Server 複寫], 系統管理考量"
  - "管理複寫, Oracle 發行"
ms.assetid: cfd81fb5-419b-4a1b-97c4-be7c9d4ee289
caps.latest.revision: 29
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 29
---
# Oracle 發行者的管理考量
  在設定「Oracle 發行者」並且複寫變更追蹤機制到位之後，Oracle 資料庫系統的管理員仍可使用標準 Oracle 資料庫公用程式並執行一般的系統管理工作。 但是，您應該留意執行特定管理工作對已發行資料的影響。  
  
 卸除或修改為複寫發行的資料行，或者卸除或修改任何複寫物件除外，這些考量不會套用至快照式發行集。  
  
## 匯入與載入資料  
 為 Oracle 上的交易式發行集變更追蹤使用觸發程序。 僅在出現更新、插入或刪除時引發複寫觸發程序的情況下，方可將對已發行資料表所作的變更複寫給「訂閱者」。 Oracle 公用程式 Oracle Import 與 SQL*Loader 均有在使用這些公用程式將資料列插入複寫資料表時，決定是否引發觸發程序的選項。  
  
### Oracle Import  
 使用 Oracle Import，您可以設定選項 **忽略** 為 y 或 n (預設值是 ' n ')。 如果 **忽略** 設為 ' n '，卸除並重新匯入期間建立的資料表。 這將會移除複寫觸發程序並停用複寫。 如果 **忽略** 設為 「 y 」，匯入將會嘗試將資料列載入現有的資料表，就會引發複寫觸發程序。 因此，請確定 **忽略** 匯入至匯入工具的複寫資料表時，設定為 'y'。  
  
### SQL*Loader  
 使用 SQL\*載入器，您可以設定選項 **直接** 為 'true' 或 'false' （預設值為 'false'）。 如果 **直接** 設為 'false'，資料列會插入使用傳統的 INSERT 陳述式，這將引發複寫觸發程序。 如果 **直接** 設為 'true'，負載會經過最佳化，並不會引發觸發程序。 因此，請確定 **直接** 設定為 'false' 當載入複寫資料表與 SQL * Loader 工具。  
  
## 變更已發行物件  
 執行下列動作無需特殊考量：  
  
-   在已發行資料表上重建索引。  
  
-   將使用者觸發程序新增至已發行資料表。  
  
 下列動作要求您停止已發行資料表上的所有活動：  
  
-   移動已發行資料表。  
  
 下列動作要求您卸除發行集、執行作業，然後重新建立發行集：  
  
-   截斷已發行資料表。  
  
-   重新命名已發行資料表。  
  
-   將資料行新增至已發行資料表。  
  
-   卸除或修改為複寫發行的資料行。  
  
-   執行非記錄作業。  
  
## 卸除或修改複寫物件  
 如果您卸除或修改任何「發行者」層級追蹤資料表、觸發程序、順序或預存程序，則必須卸除並重新設定「發行者」。 這些物件的部分清單，請參閱 [物件建立於 「 Oracle 發行者 」 上](../../../relational-databases/replication/non-sql/objects-created-on-the-oracle-publisher.md)。  
  
 如需詳細資訊卸除和重新設定 「 發行者 」，一節 「 變更需要重新設定發行者 」 主題中 [Oracle 發行者疑難排解](../../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md)。  
  
## 另請參閱  
 [設定 Oracle 發行者](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Oracle 發行者的設計考量與限制](../../../relational-databases/replication/non-sql/design-considerations-and-limitations-for-oracle-publishers.md)   
 [Oracle 發行概觀](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  
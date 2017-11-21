---
title: "hierarchyid (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- hierarchyid
- hierarchyid_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Hierarchy data type
- hierarchyid data type
ms.assetid: 69b756e0-a1df-45b3-8a24-6ded8658aefe
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 44299e7ddb90bdd52e2638dd859993513bd6f966
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="hierarchyid-data-type-method-reference"></a>hierarchyid 資料類型方法參考
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

**Hierarchyid**資料類型是可變長度的系統資料類型。 使用**hierarchyid**來代表階層中的位置。 **hierarchyid** 類型的資料行不會自動代表樹狀目錄。 應用程式負責決定是否要產生並指派 **hierarchyid** 值，以便讓資料列之間所需的關聯性反映在值中。
  
**hierarchyid** 資料類型的值代表樹狀目錄階層中的位置。 **hierarchyid** 的值具有下列屬性：
  
-   極度壓縮  
     代表樹狀目錄 (含有 *n* 個節點) 中之節點所需的平均位元數目會因平均扇出 (節點子系的平均數目) 而不同。 小型 fanout (0-7)，大小大約是 6\*logA *n* 位元，其中 A 是平均 fanout。 在平均 fanout 為 6 個階層之 100,000 人員的組織階層中，節點會佔用大約 38 位元。 然後，這會四捨五入成 40 位元 (或 5 個位元組)，以便進行儲存。  
-   比較是按照深度優先順序  
     假設有兩個 **hierarchyid** 值 (**a** 和 **b**)，**a<b** 就表示在樹狀目錄的深度優先周遊中，a 在 b 前面。 **hierarchyid** 資料類型的索引採用深度優先順序，而且在深度優先周遊中彼此接近的節點會以彼此接近的方式儲存。 例如，某筆記錄的子系會儲存在該記錄旁。 如需詳細資訊，請參閱[階層式資料 &#40;SQL Server &#41;](../../relational-databases/hierarchical-data-sql-server.md).  
-   支援任意插入和刪除  
     透過使用 [GetDescendant](../../t-sql/data-types/getdescendant-database-engine.md) 方法，您就一定能夠在任何指定節點的右側、任何指定節點的左側，或任何兩個同層級之間產生同層級。 在階層中插入或刪除任意的節點數目時，比較屬性會保留下來。 大部分的插入和刪除項目都會保留壓縮度屬性。 不過，兩個節點之間的插入項目則會以稍微少的壓縮表示來產生 hierarchyid 值。  
-   使用中的編碼方式**hierarchyid**型別是限制為 892 個位元組。 因此，具有在其表示法，而無法放入 892 個位元組的層級太多的節點無法由**hierarchyid**型別。  
  
**Hierarchyid**型別是供 CLR 用戶端，做為**SqlHierarchyId**資料型別。
  
## <a name="remarks"></a>備註  
**Hierarchyid**類型編碼從樹狀結構的根節點的路徑以邏輯方式編碼階層樹狀結構中的單一節點的相關資訊。 這類路徑會以邏輯方式表示成在根目錄之後造訪之所有子系的節點標籤序列。 此表示以斜線為開頭，而且只有造訪根目錄的路徑才會以單一斜線表示。 若為根目錄底下的層級，每個標籤都會編碼成以小數點隔開的整數序列。 子系之間的比較是透過按照字典順序比較以小數點隔開的整數序列加以執行。 每個層級後面都跟著一個斜線。 因此，斜線會分隔父代與其子系。 例如，以下是有效**hierarchyid**路徑的長度為 1、 2、 2、 3 和 3 分別層級：
  
-   /  
  
-   /1/  
  
-   /0.3.-7/  
  
-   /1/3/  
  
-   /0.1/0.2/  
  
您可以在任何位置插入節點。 節點後插入**/1/2/**前**/1/3/**可以表示成**/1/2.5/**。 在 0 之前插入的節點具有負數的邏輯表示。 例如，前面的節點**/1/1/**可以表示成**/1 /-1 /**。 節點不能有前置零。 例如， **/1/1.1/**有效，但**/1/1.01/**不正確。 若要避免這個錯誤，請使用插入節點[GetDescendant](../../t-sql/data-types/getdescendant-database-engine.md)方法。
  
## <a name="data-type-conversion"></a>資料類型轉換
**Hierarchyid**資料類型可以轉換成其他資料類型，如下所示：
-   使用[tostring （)](../../t-sql/data-types/tostring-database-engine.md)方法，將轉換**hierarchyid**值的邏輯表示**nvarchar （4000)**資料型別。  
-   使用[讀取 （）](../../t-sql/data-types/read-database-engine.md)和[Write （)](../../t-sql/data-types/write-database-engine.md)轉換**hierarchyid**至**varbinary**。  
-   傳輸**hierarchyid**透過 SOAP 參數先轉換成字串。  
  
## <a name="upgrading-databases"></a>升級資料庫
當資料庫升級為[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，新的組件和**hierarchyid**資料類型會自動安裝。 Upgrade Advisor 規則會偵測任何具有衝突名稱的使用者類型或組件。 Upgrade Advisor 將建議您重新命名任何衝突的組件，以及重新命名任何衝突的類型，或在程式碼中使用兩部分名稱來參考預先存在的使用者類型。
  
如果資料庫升級偵測到具有衝突名稱的使用者組件，它將自動重新命名該組件並讓資料庫進入質疑模式。
  
如果具有衝突名稱的使用者類型在升級期間存在，將不會採取任何特殊步驟。 在升級之後，舊的使用者類型和新的系統類型都會一起存在。 但是，該使用者類型只能透過兩部分名稱使用。
  
## <a name="using-hierarchyid-columns-in-replicated-tables"></a>在複寫資料表中使用 hierarchyid 資料行
類型的資料行**hierarchyid**可用在任何複寫的資料表上。 您應用程式的需求會因複寫是單向或雙向，以及使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本而不同。
  
### <a name="one-directional-replication"></a>單向複寫
單向複寫包括快照式複寫、異動複寫，以及不在「訂閱者」端進行變更的合併式複寫。 如何**用**資料行使用單向覆寫的版本取決於[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]「 訂閱者 」 正在執行。
-   A[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]可以複寫發行者**用**欄[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]訂閱者沒有任何特殊考量。  
-   A[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]發行者必須轉換**hierarchyid**資料行，以將它們複寫至訂閱者 」 執行[!INCLUDE[ssEW](../../includes/ssew-md.md)]或較早版本的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 [!INCLUDE[ssEW](../../includes/ssew-md.md)]和舊版的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不支援**hierarchyid**資料行。 如果您正使用其中一個版本，仍然可以將資料複寫至「訂閱者」。 若要這樣做，您必須設定結構描述選項或發行集相容性層級 (用於合併式複寫)，如此資料行才能轉換成相容的資料類型。  
  
在這兩種情況下都支援資料行篩選。 這包括篩選出**hierarchyid**資料行。 資料列篩選，只要篩選不包括支援**hierarchyid**資料行。
  
### <a name="bi-directional-replication"></a>雙向複寫
雙向複寫包括具有更新訂閱的異動複寫、點對點異動複寫，以及在「訂閱者」端進行變更的合併式複寫。 複寫可讓您設定具有資料表**hierarchyid**雙向複寫的資料行。 請注意下列需求和考量。
-   「發行者」和所有「訂閱者」都必須執行 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
-   複寫會將資料複寫成位元組，但不會執行任何驗證來確保階層的完整性。  
-   在來源 (「訂閱者」或「發行者」) 進行的變更複寫到目的地時，將不會維持這些變更的階層。  
-   雜湊值**hierarchyid**特有的資料庫產生的資料行。 因此，雖然可以在「發行者」和「訂閱者」上產生相同的值，但是它可能會套用至不同的資料列。 複寫不會檢查此條件，並沒有任何內建方法，分割區**hierarchyid**資料行值，因為沒有針對識別資料行。 應用程式必須使用條件約束或其他機制來避免發生這類無法偵測的衝突。  
-   在「訂閱者」端插入的資料列可能會被遺棄。 已插入資料列的父資料列可能已經在「發行者」端遭刪除了。 當「訂閱者」的資料列在「發行者」端插入時，這會導致無法偵測的衝突發生。  
-   資料行篩選無法篩選出不可為 null **hierarchyid**資料行： 來自訂閱者端的插入會失敗，因為沒有預設值為**hierarchyid** 「 發行者 」 端的資料行。  
-   資料列篩選，只要篩選不包括支援**hierarchyid**資料行。  
  
## <a name="see-also"></a>另請參閱
[階層式資料 &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[Hierarchyid 資料類型方法參考](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)
  
  


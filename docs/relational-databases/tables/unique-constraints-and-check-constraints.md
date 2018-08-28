---
title: 唯一條件約束與檢查條件約束 | Microsoft 文件
ms.custom: ''
ms.date: 06/27/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- constraints [SQL Server], Visual Database Tools
- Visual Database Tools [SQL Server], constraints
ms.assetid: 637098af-2567-48f8-90f4-b41df059833e
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 09ac96ccc139514a1845bb2a4455d6e8f30dc3a8
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43078820"
---
# <a name="unique-constraints-and-check-constraints"></a>唯一條件約束與檢查條件約束
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  UNIQUE 和 CHECK 是兩種類型的條件約束，可用來強制執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表中的資料完整性。 這些都是重要的資料庫物件。  
  
 本主題包含下列各節。  
  
 [UNIQUE 條件約束](#Unique)  
  
 [CHECK 條件約束](#Check)  
  
 [相關工作](#Tasks)  
  
##  <a name="Unique"></a> UNIQUE 條件約束  
 條件約束是 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 為您強制執行的規則。 例如，您可以使用 UNIQUE 條件約束，確定在未參與主索引鍵的特定資料行中沒有重複值。 雖然 UNIQUE 條件約束和 PRIMARY KEY 條件約束兩者都強制唯一性，但是當您想要強制非主索引鍵之資料行 (或資料行組合) 的唯一性時，請使用 UNIQUE 條件約束而不要使用 PRIMARY KEY 條件約束。  
  
 UNIQUE 條件約束允許 NULL 值，這與 PRIMARY KEY 條件約束不同。 但是，就像參與 UNIQUE 條件約束的任何值，一個資料行只能有一個 Null 值。 UNIQUE 條件約束也可被 FOREIGN KEY 條件約束所參考。  
  
 當 UNIQUE 條件約束加入資料表現有的一個或多個資料行時， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會檢查資料行中的現有資料，以確保所有數值都是唯一的。 如果將 UNIQUE 條件約束加入包含重複數值的資料行內， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會傳回錯誤訊息，而且不加入條件約束。  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 將自動建立 UNIQUE 索引，以強制執行 UNIQUE 條件約束的唯一性要求。 因此，如果嘗試插入重複的資料列， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會傳回錯誤訊息，告訴您違反了 UNIQUE 條件約束，並且不會將資料列加入資料表內。 除非明確設定叢集索引，否則預設會建立一個非叢集索引來執行 UNIQUE 條件約束。  
  
##  <a name="Check"></a> CHECK 條件約束  
 CHECK 條件約束限制一個或多個資料行接受的值，藉此強制值域完整性。 您可使用能根據邏輯運算子傳回 TRUE 或 FALSE 的任何邏輯 (布林) 運算式來建立 CHECK 條件約束。 例如，可以藉由建立只允許範圍從 $15,000 到 $100,000 之資料的 CHECK 條件約束，以限制 **salary** 資料行的值範圍。 這可防止輸入的薪水超過一般的薪水範圍。 邏輯運算式可以是： `salary >= 15000 AND salary <= 100000`。  
  
 您可以將多個 CHECK 條件約束套用到單一資料行。 您也可以在資料表層級建立單一 CHECK 條件約束，將它套用到多個資料行。 例如，多重資料行的 CHECK 條件約束可用來確認 **country_region** 資料行值為 **USA** 的任何資料列，其 **state** 資料行內也會有兩個字元的值。 這允許可在某一個位置上檢查多個條件。  
  
 CHECK 條件約束類似於 FOREIGN KEY 條件約束，用來控制放入資料行的值。 其間的差異在於它們如何判定哪些值有效：FOREIGN KEY 條件約束從另一個資料表取得有效值清單，而 CHECK 條件約束則會從邏輯運算式來判定有效值。  
  
> [!CAUTION]  
>  包括明確或隱含資料類型轉換的條件約束可能會導致某些作業失敗。 例如，在資料分割切換來源的資料表上所定義的此類條件約束，可能會導致 ALTER TABLE...SWITCH 作業失敗。 應避免在條件約束定義中進行資料類型轉換。  
  
### <a name="limitations-of-check-constraints"></a>CHECK 條件約束的限制  
 CHECK 條件約束會拒絕評估為 FALSE 的值。 因為 Null 值會評估為 UNKNOWN，所以若其出現於運算式中，可能會覆寫條件約束。 例如，假設您將條件約束放在 **int** 資料行 **MyColumn** 中，指定 **MyColumn** 只能包含 10 這個值 (**MyColumn=10**)。 如果您將 NULL 值插入 **MyColumn**，則 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會插入 NULL 且不會傳回錯誤。  
  
 CHECK 條件約束會針對資料表中的所有資料列進行檢查，當檢查的條件不為 FALSE 時，會傳回 TRUE。 CHECK 條件約束可在資料列層級運作。 如果剛建立的資料表沒有任何資料列，則這個資料表上的任何 CHECK 條件約束都將視為有效。 這種情況可能會產生非預期結果，如下列範例所示。  
  
```  
CREATE TABLE CheckTbl (col1 int, col2 int);  
GO  
CREATE FUNCTION CheckFnctn()  
RETURNS int  
AS   
BEGIN  
   DECLARE @retval int  
   SELECT @retval = COUNT(*) FROM CheckTbl  
   RETURN @retval  
END;  
GO  
ALTER TABLE CheckTbl  
ADD CONSTRAINT chkRowCount CHECK (dbo.CheckFnctn() >= 1 );  
GO  
```  
  
 要加入的 `CHECK` 條件約束會指定 `CheckTbl`資料表中至少要有一個資料列。 不過，因為資料表中沒有任何資料列，能據以檢查這個條件約束的條件，所以 ALTER TABLE 陳述式會成功執行。  
  
 CHECK 條件約束不會在 DELETE 陳述式執行期間進行驗證。 因此，若在具有某些類型之 CHECK 條件約束的資料表上執行 DELETE 陳述式，可能會產生非預期的結果。 例如，考慮在 `CheckTbl`資料表上執行的下列陳述式。  
  
```  
INSERT INTO CheckTbl VALUES (10, 10);  
GO  
DELETE CheckTbl WHERE col1 = 10;  
```  
  
 即使 `DELETE` 條件約束會指定資料表 `CHECK` 至少必須具有 `CheckTbl` 個資料列， `1` 陳述式也會執行成功。  
  
##  <a name="Tasks"></a> 相關工作  
  
> [!NOTE]  
>  如果資料表是要發佈以進行複寫，則必須使用 Transact-SQL 陳述式 [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) 或 SQL Server 管理物件 (SMO) 變更結構描述。 使用 [資料表設計工具] 或 [資料庫圖表設計工具] 變更結構描述時，會嘗試卸除並重新建立資料表。 您無法卸除已發行的物件，因此結構描述變更將會失敗。  
  
|工作|主題|  
|----------|-----------|  
|描述如何建立唯一的條件約束。|[建立唯一的條件約束](../../relational-databases/tables/create-unique-constraints.md)|  
|描述如何修改唯一的條件約束。|[修改唯一的條件約束](../../relational-databases/tables/modify-unique-constraints.md)|  
|描述如何刪除唯一條件約束。|[刪除唯一的條件約束](../../relational-databases/tables/delete-unique-constraints.md)|  
|描述如何在複寫代理程式在資料表中插入或更新資料時，停用檢查條件約束。|[停用複寫的檢查條件約束](../../relational-databases/tables/disable-check-constraints-for-replication.md)|  
|描述如何在加入資料表資料、更新資料表資料或刪除資料表資料時，停用檢查條件約束。|[使用 INSERT 與 UPDATE 陳述式停用檢查條件約束](../../relational-databases/tables/disable-check-constraints-with-insert-and-update-statements.md)|  
|描述如何變更條件約束運算式或啟用或停用特定條件之條件約束的選項。|[修改檢查條件約束](../../relational-databases/tables/modify-check-constraints.md)|  
|描述如何刪除檢查條件約束。|[刪除檢查條件約束](../../relational-databases/tables/delete-check-constraints.md)|  
|描述如何檢視檢查條件約束的屬性。|[唯一條件約束與檢查條件約束](../../relational-databases/tables/unique-constraints-and-check-constraints.md)|  
  
  

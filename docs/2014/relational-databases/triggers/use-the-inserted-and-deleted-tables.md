---
title: 使用插入或刪除的資料表 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- inserted tables
- UPDATE statement [SQL Server], DML triggers
- DELETE statement [SQL Server], DML triggers
- INSTEAD OF triggers
- deleted tables
- INSERT statement [SQL Server], DML triggers
- DML triggers, deleted or inserted tables
ms.assetid: ed84567f-7b91-4b44-b5b2-c400bda4590d
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: bc9bb9b663841641c88d61ffce0073de658b334d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48220939"
---
# <a name="use-the-inserted-and-deleted-tables"></a>使用插入或刪除的資料表
  DML 觸發程序陳述式使用兩個特殊的資料表：已刪除的資料表和已插入的資料表。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會自動建立及管理這些資料表。 您可以使用這些暫存、常駐記憶體的資料表來測試某些資料修改的效果，以及設定 DML 觸發程序動作的條件。 您無法直接修改這些資料表的資料，或是在這些資料表上執行資料定義語言 (DDL) 作業，例如 CREATE INDEX。  
  
 在 DML 觸發程序中，inserted 和 deleted 資料表主要是用來執行下列動作：  
  
-   擴充資料表之間的參考完整性。  
  
-   在檢視底下的基底資料表中插入或更新資料。  
  
-   測試錯誤，並根據錯誤採取動作。  
  
-   尋找資料修改前後之資料表狀態的差異，並依據這些差異採取動作。  
  
 deleted 資料表會儲存被 DELETE 及 UPDATE 陳述式影響的資料列副本。 在執行 DELETE 或 UPDATE 陳述式時，資料列會從觸發程序資料表刪除，並傳送到 deleted 資料表。 deleted 資料表及其觸發程序資料表兩者通常不會有資料列。  
  
 inserted 資料表會儲存被 INSERT 及 UPDATE 陳述式影響的資料列副本。 在插入或更新交易期間，新的資料列會同時加入 inserted 資料表和觸發程序資料表。 inserted 資料表中的資料列即為觸發程序資料表中新資料列的副本。  
  
 更新交易就像是刪除後再插入的動作；首先，舊資料列被複製到 deleted 資料表，接著將新資料列再複製到觸發程序資料表以及 inserted 資料表。  
  
 設定觸發程序的條件時，可以適當地利用 inserted 與 deleted 資料表設定引發觸發條件的動作。 雖然參考 deleted 資料表來測試 INSERT 陳述式或是參考 inserted 資料表測試 DELETE 陳述式時，並不會有任何錯誤發生，但在這種情形下，觸發程序測試資料表內將不會有任何資料列產生。  
  
> [!NOTE]  
>  若觸發程序動作依據被修改的資料列數目來決定啟動與否時，則可利用對多資料列資料修改 (依據 SELECT 陳述式的 INSERT、DELETE 或 UPDATE) 的測試 (如 @@ROWCOUNT 的檢查)，以決定執行何者動作。  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 在使用 AFTER 觸發程序時，不允許參考 inserted 和 deleted 資料表中的 `text`、`ntext` 或 `image` 資料行。 但還是包含這些資料類型，僅做為回溯相容性的目的使用。 對於大量資料，較佳的儲存方式是使用 `varchar(max)`、`nvarchar(max)` 和 `varbinary(max)` 資料類型。 AFTER 和 INSTEAD OF 觸發程序都支援 inserted 和 deleted 資料表中的 `varchar(max)`、`nvarchar(max)` 和 `varbinary(max)` 資料。 如需詳細資訊，請參閱 [CREATE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql)。  
  
 **在觸發程序中使用 inserted 資料表來強制執行商務規則的範例**  
  
 由於 CHECK 條件約束只能參考定義了資料行層級或資料表層級條件約束的資料行，任何跨資料表的條件約束 (這裡是商務規則) 都必須定義成觸發程序。  
  
 下列範例會建立一個 DML 觸發程序。 當試圖在 `PurchaseOrderHeader` 資料表中插入新的採購單時，這個觸發程序會檢查確認供應商的信用等級良好。 若要取得對應至剛插入之採購單的供應商信用等級，您必須參考 `Vendor` 資料表，而此資料表也必須與 inserted 資料表聯結。 如果信用等級太低，將會顯示訊息，且不會執行插入動作。 請注意此範例不允許進行多資料列資料修改。 如需詳細資訊，請參閱 [建立 DML 觸發程序以處理多重資料列](../triggers/create-dml-triggers-to-handle-multiple-rows-of-data.md)。  
  
 [!code-sql[TriggerDDL#CreateTrigger3](../../snippets/tsql/SQL14/tsql/triggerddl/transact-sql/snippet_create_alter_drop_trigger.sql#createtrigger3)]  
  
## <a name="using-the-inserted-and-deleted-tables-in-instead-of-triggers"></a>在 INSTEAD OF 觸發程序中使用已插入與已刪除的資料表  
 傳遞到依據資料表定義的 INSTEAD OF 觸發程序之 inserted 及 deleted 資料表，會與傳遞到 AFTER 觸發程序的 inserted 及 deleted 資料表遵循相同的規則。 inserted 及 deleted 資料表的格式，與據以定義 INSTEAD OF 觸發程序的資料表格式相同。 inserted 及 deleted 資料表中的每一資料行，都會直接對應到基底資料表中的資料行。  
  
 下列規則是有關參考含 INSTEAD OF 觸發程序之資料表的 INSERT 或 UPDATE 陳述式何時必須提供資料行值，即使資料表不含 INSTEAD OF 觸發程序時也一樣：  
  
-   無法為計算的資料行或資料類型為 `timestamp` 的資料行指定值。  
  
-   除非資料表的 IDENTITY_INSERT 是 ON，否則無法為帶有 IDENTITY 屬性的資料表指定值。 當 IDENTITY_INSERT 為 ON 時，INSERT 陳述式必須提供一個值。  
  
-   INSERT 陳述式必須為不含 DEFAULT 條件約束的所有 NOT NULL 資料行提供值。  
  
-   除了計算、 識別或`timestamp`資料行值都是選擇性的任何資料行允許 null，或任何 NOT NULL 資料行有預設定義。  
  
 當 INSERT、UPDATE 或 DELETE 陳述式參考含有 INSTEAD OF 觸發程序的檢視時， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會呼叫觸發程序，而不會直接對任何資料表採取任何動作。 觸發程序必須使用 inserted 及 deleted 資料表中的資訊，來建立實作基底資料表中要求的動作所需的陳述式，即使為檢視所建立的 inserted 及 deleted 資料表中的資訊格式與基底資料表中的資料格式並不相同也一樣。  
  
 傳遞給定義在檢視上 INSTEAD OF 觸發程序的 inserted 及 deleted 資料表格式，必須與針對檢視定義的 SELECT 陳述式之選取清單相符。 例如：  
  
```  
USE AdventureWorks2012;  
GO  
CREATE VIEW dbo.EmployeeNames (BusinessEntityID, LName, FName)  
AS  
SELECT e.BusinessEntityID, p.LastName, p.FirstName  
FROM HumanResources.Employee AS e   
JOIN Person.Person AS p  
ON e.BusinessEntityID = p.BusinessEntityID;  
```  
  
 這個檢視的結果集有三個資料行：一個 `int` 資料行和兩個 `nvarchar` 資料行。 傳遞給在檢視表上定義之 INSTEAD OF 觸發程序的 inserted 和 deleted 資料表，也必須有名稱為 `BusinessEntityID` 的 `int` 資料行、名稱為 `LName` 的 `nvarchar` 資料行，以及名稱為 `FName` 的 `nvarchar` 資料行。  
  
 檢視的選取清單也可以包含不直接對應到單一基底資料表資料行的運算式。 有些檢視運算式，例如條件約束或函數引動過程，無法參考任何資料行且可以被忽略。 複雜運算式可以參考多個資料行，但 inserted 及 deleted 資料表的每個插入資料列只能有一個值。 同樣的原則亦適用於檢視中的簡單運算式，前提是它們參考的計算資料行含有複雜運算式。 檢視的 INSTEAD OF 觸發程序必須處理這些類型的運算式。  
  
  

---
description: DML 觸發程序
title: DML 觸發程序 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- triggers [SQL Server], about triggers
- DML triggers, about DML triggers
- triggers [SQL Server]
ms.assetid: 298eafca-e01f-4707-8c29-c75546fcd6b0
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 27776324d94176619c25acbeefb3b6bd901d8a2a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418932"
---
# <a name="dml-triggers"></a>DML 觸發程序
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  DML 觸發程序是一種特殊類型的預存程序，會在影響觸發程序中所定義之資料表或檢視表的資料操作語言 (DML) 事件執行時自動執行。 DML 事件包括 INSERT、UPDATE 或 DELETE 陳述式。 DML 觸發程序可用以強制執行商務規則和資料完整性、查詢其他資料表，以及包括複雜的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。 觸發程序和引發它的陳述式會被視為單一交易處理，而這樣的交易可以從觸發程序內部回復。 如果偵測到伺服器錯誤 (例如，磁碟空間不足)，整個交易就會自動回復。  
  
## <a name="dml-trigger-benefits"></a>DML 觸發程序的優點  
 DML 觸發程序與條件約束類似，兩者都可強制執行實體完整性或網域完整性。 實體完整性一般應由最低層級的索引強制執行，且應為 PRIMARY KEY 和 UNIQUE 條件約束的一部分，或是與條件約束完全無關。 網域完整性應透過 CHECK 條件約束來強制執行，而參考完整性 (RI) 則應透過 FOREIGN KEY 條件約束來強制執行。 當條件約束所支援的功能無法滿足應用程式的功能需求時，DML 觸發程序即可發揮它的作用。  
  
 下列清單比較 DML 觸發程序與條件約束，以及識別較適合使用 DML 觸發程序的時間。  
  
-   DML 觸發程序可以串聯資料庫中相關資料表的變更，不過，使用串聯的參考完整性條件約束來執行這些變更會更有效率。 除非 REFERENCES 子句定義串聯的參考動作，否則 FOREIGN KEY 條件約束只能透過與另一資料行中的值完全相符的值來驗證資料行值。  
  
-   它們可以預防惡意或錯誤的 INSERT、UPDATE 和 DELETE 作業，並且強制執行其他比 CHECK 條件約束所定義的限制更複雜的限制。  
  
     與 CHECK 條件約束不同的是，DML 觸發程序可以參考其他資料表中的資料行。 例如，觸發程序可以使用其他資料表的 SELECT 來比較插入或更新的資料，以及執行其他動作，如修改資料或顯示使用者自訂錯誤訊息。  
  
-   它們可以評估資料修改前後的資料表狀態，並依據這些差異採取動作。  
  
-   資料表中相同類型 (INSERT、UPDATE 或 DELETE) 的多個 DML 觸發程序，允許對相同的修改陳述式執行多種不同的動作。  
  
-   條件約束只能傳達標準化的系統錯誤訊息。 如果您的應用程式需要或有必要取得自訂訊息及更為詳盡的錯誤處理訊息，則您必須使用觸發程序。  
  
-   DML 觸發程序可不允許或可復原違反參考完整性的變更，因此會取消嘗試進行的資料修改。 像這樣的觸發程序會在您變更外部索引鍵以及新值與其主索引鍵不相符時產生效果。 然而，FOREIGN KEY 條件約束通常用於此目的。  
  
-   如果觸發資料表有條件約束的話，它們會在執行 INSTEAD OF 觸發程序後，但在執行 AFTER 觸發程序前檢查。 如果違反條件約束的話，即復原 INSTEAD OF 觸發程序動作，並且不執行 AFTER 觸發程序。  
  
## <a name="types-of-dml-triggers"></a>DML 觸發程序的類型  
 AFTER 觸發程序  
 AFTER 觸發程序會在執行過 INSERT、UPDATE、MERGE 或 DELETE 陳述式的動作後才執行。 發生強制違規時絕對不會執行 AFTER 觸發程序，所以，這些觸發程序無法用於可能妨礙強制違規的任何處理動作。 對於 MERGE 陳述式中指定的每個 INSERT、UPDATE 或 DELETE 動作，會針對每一項 DML 作業引發對應的觸發程序。  
  
 INSTEAD OF 觸發程序。  
 INSTEAD OF 觸發程序會覆寫觸發陳述式的標準動作。 因此，它們可以用於對一個或多個資料行執行錯誤或值檢查，然後在插入、更新或刪除一個或多個資料列之前執行其他動作。 例如，更新薪資資料表中的時薪值時，可以定義一個觸發程序，讓它在超過指定的值時產生錯誤訊息並回復交易，或是先在薪資資料表中插入記錄，然後將新的記錄插入稽核記錄。 INSTEAD OF 觸發程序最主要的優點，就是讓無法更新的檢視支援更新。 例如，以多個基底資料表為基礎的檢視必須使用 INSTEAD OF 觸發程序以支援在多個資料表中參考資料的插入、更新與刪除動作。 INSTEAD OF 觸發程序的另一項優點在於讓您編寫邏輯時可拒絕批次的某些部分，讓批次的其他部分成功執行。  
  
 下表比較 AFTER 與 INSTEAD OF 觸發程序的功能。  
  
|函式|AFTER 觸發程序|INSTEAD OF 觸發程序。|  
|--------------|-------------------|------------------------|  
|適用性|資料表|資料表與檢視|  
|每個資料表或檢視的數量|每個觸發動作 (UPDATE、DELETE 與 INSERT) 有多個|每個觸發動作 (UPDATE、DELETE 與 INSERT) 各一個|  
|串聯參考|沒有限制|INSTEAD OF UPDATE 及 DELETE 觸發程序不允許用於串聯參考完整性條件約束的目標資料表。|  
|執行|之後：<br /><br /> 條件約束處理<br /><br /> 宣告性參考動作<br /><br /> **inserted** 與 **deleted** 資料表建立<br /><br /> 觸發動作|之前：條件約束處理<br /><br /> 取代：觸發動作<br /><br /> 之後：  **inserted** 與 **deleted** 資料表建立|  
|執行順序|可指定第一和最後一個執行|不適用|  
|**已插入**和 **已刪除**資料表中的 **varchar(max)** 、 **nvarchar(max)** 和 **varbinary(max)** 資料行參考|允許|允許|  
|**已插入**和 **已刪除**資料表中的 **text** 、 **ntext** 和 **image** 資料行參考|不允許|允許|  
  
 CLR 觸發程序  
 CLR 觸發程序可以是 AFTER 或 INSTEAD OF 觸發程序。 CLR 觸發程序也可以是 DDL 觸發程序。 CLR 觸發程序不執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序，而是執行以 Managed 程式碼撰寫的一個或多個方法，這些方法是在 .NET Framework 中建立並在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中上傳的組件成員。  
  
## <a name="related-tasks"></a>相關工作  
  
|Task|主題|  
|----------|-----------|  
|描述如何建立 DML 觸發程序。|[建立 DML 觸發程序](../../relational-databases/triggers/create-dml-triggers.md)|  
|描述如何建立 CLR 觸發程序。|[建立 CLR 觸發程序](../../relational-databases/triggers/create-clr-triggers.md)|  
|描述如何建立 DML 觸發程序以處理單一資料列和多資料列資料修改。|[建立 DML 觸發程序以處理多重資料列](../../relational-databases/triggers/create-dml-triggers-to-handle-multiple-rows-of-data.md)|  
|描述如何巢狀化觸發程序。|[建立巢狀觸發程序](../../relational-databases/triggers/create-nested-triggers.md)|  
|描述如何指定 AFTER 觸發程序的引發順序。|[指定第一個與最後一個觸發程序](../../relational-databases/triggers/specify-first-and-last-triggers.md)|  
|描述如何在觸發程序程式碼中使用特殊插入和刪除資料表。|[使用插入或刪除的資料表](../../relational-databases/triggers/use-the-inserted-and-deleted-tables.md)|  
|描述如何修改或重新命名 DML 觸發程序。|[修改或重新命名 DML 觸發程序](../../relational-databases/triggers/modify-or-rename-dml-triggers.md)|  
|描述如何檢視有關 DML 觸發程序的資訊。|[取得關於 DML 觸發程序的詳細資訊](../../relational-databases/triggers/get-information-about-dml-triggers.md)|  
|描述如何刪除或停用 DML 觸發程序。|[刪除或停用 DML 觸發程序](../../relational-databases/triggers/delete-or-disable-dml-triggers.md)|  
|描述如何管理觸發程序安全性。|[管理觸發程序安全性](../../relational-databases/triggers/manage-trigger-security.md)|  
  
## <a name="see-also"></a>另請參閱  
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [DROP TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [DISABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/disable-trigger-transact-sql.md)   
 [觸發程序函數 &#40;Transact-SQL&#41;](../../t-sql/functions/trigger-functions-transact-sql.md)  
  
  

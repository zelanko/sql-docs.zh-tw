---
title: MSSQLSERVER_1505 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 1505 (Database Engine error)
ms.assetid: ef4df75d-0f36-4c8b-b36c-e427f65f91ca
caps.latest.revision: 14
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 8383fd472e054f26db78ab8ec28b4a67e81e7f02
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver1505"></a>MSSQLSERVER_1505
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|1505|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DUP_KEY|  
|訊息文字|發現物件名稱 '%.*ls' 和索引名稱 '%.\*ls' 的重複索引鍵，CREATE UNIQUE INDEX 已結束。  重複的索引鍵值為 %ls。|  
  
## <a name="explanation"></a>說明  
當您嘗試建立唯一索引，而且資料表中的多個資料列包含指定的重複值時，就會發生這項錯誤。 當您建立索引並指定 UNIQUE 關鍵字，或者建立 UNIQUE 條件約束時，就會建立唯一索引。 資料表無法包含在索引或條件約束中定義的資料行內具有重複值的任何資料列。  
  
請考慮下列 **Employee** 資料表中的資料：  
  
|LastName|FirstName|JobTitle|HireDate|  
|------------|-------------|------------|------------|  
|Walters|Rob|Senior Tool Designer|2004-11-19|  
|Brown|Kevin|Marketing Assistant|NULL|  
|Brown|Jo|Design Engineer|NULL|  
|Walters|Rob|Tool Designer|2001-08-09|  
  
由於資料列含有重複值，因此無法在資料行組合 **LastName** 或 **LastName**、**FirstName** 上建立唯一索引。  
  
**HireDate** 資料行違反唯一性的可能較不明顯。 執行索引時，NULL 值會當做相等值進行比較。 因此，如果有多個資料行中的索引鍵值為 NULL，您就無法建立唯一索引或條件約束。 基於上述資料，因此您無法在資料行組合 **HireDate** 或 **LastName**、**HireDate** 上建立唯一索引。  
  
錯誤訊息 1505 會傳回違反唯一性條件約束的第一個資料列。 資料表可能含有其他重複的資料列。 若要尋找所有重複的資料列，請查詢指定的資料表並使用 GROUP BY 和 HAVING 子句來報告重複的資料列。 例如，下列查詢會傳回 **Employee** 資料表中具有重複名字和姓氏的資料列。  
  
SELECT LastName, FirstName, count(*) FROM dbo.Employee GROUP BY LastName, FirstName HAVING count(\*) > 1;  
  
## <a name="user-action"></a>使用者動作  
請考慮下列解決方案。  
  
-   在索引或條件約束定義中加入或移除資料行，以便建立唯一複合索引。 在上述範例中，於索引或條件約束定義中新增 **MiddleName** 資料行，應該就可以解決重複值的問題。  
  
-   當您選擇唯一索引或條件約束的資料行時，請選取已定義為 NOT NULL 的資料行。 這樣做可以排除多個資料列的索引鍵值包含 NULL 而導致違反唯一性的可能。  
  
-   若重複值是因資料輸入錯誤所造成，請手動更正資料，然後再建立索引或約束條件。 如需在資料表中移除重複資料列的詳細資訊，請參閱知識庫文件 139444：[How to remove duplicate rows from a table in SQL Server](http://support.microsoft.com/kb/139444)(如何在 SQL Server 中移除資料表中的重複資料列)。  
  
## <a name="see-also"></a>另請參閱  
[CREATE INDEX &#40;Transact-SQL&#41;](~/t-sql/statements/create-index-transact-sql.md)  
[建立唯一索引](~/relational-databases/indexes/create-unique-indexes.md)  
[建立唯一的條件約束](~/relational-databases/tables/create-unique-constraints.md)  
  


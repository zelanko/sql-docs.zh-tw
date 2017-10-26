---
title: "撰寫國際通用的 Transact-SQL 陳述式 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- writing international statements
- Transact-SQL international considerations
- international considerations [SQL Server], Transact-SQL
- Database Engine international considerations [SQL Server], Transact-SQL
- statements [SQL Server], international
- database international considerations [SQL Server], Transact-SQL
- dates [SQL Server], international considerations
ms.assetid: f0b10fee-27f7-45fe-aece-ccc3f63bdcdb
caps.latest.revision: 35
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8c73a4b7e8d9c3e470136942c830a0ba879ed420
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="write-international-transact-sql-statements"></a>撰寫國際通用的 Transact-SQL 陳述式
  如果遵循下列的指導方針，使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的資料庫與資料庫應用程式將更能從一個語言移植至另一個語言，或可支援多種語言：  
  
-   使用 **nchar**、 **nvarchar**，和 **nvarchar(max)** 來取代所有 **char**、 **varchar**，和 **text**資料類型。 如此一來您就不需要考慮字碼頁轉換的問題。 如需詳細資訊，請參閱 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)。  
  
-   當您執行月份和週中日的比較和運算時，請使用數值的日期部分，而不要使用名稱字串。 不同的語言設定會傳回不同的月份和週中日名稱。 例如，語言設定為「英文 (美國)」時，DATENAME(MONTH,GETDATE()) 會傳回 May；當語言設定為「德文」時，會傳回 Mai；而當語言設定為「法文」時，會傳回 mai。 請改用如 DATEPART 的函數，使用數字月份而不用名稱。 當您要將結果集顯示給使用者時，請使用 DATEPART 名稱，因為日期名稱通常比數值表示法來得有意義。 但是，不要根據特定語言的顯示名稱來撰寫程式碼邏輯。  
  
-   當您在比較或輸入至 INSERT 或 UPDATE 陳述式中指定日期時，請使用所有語言設定都作相同解譯的常數：  
  
    -   ADO、OLE DB 和 ODBC 應用程式應該使用以下形式的 ODBC 時間戳記、日期和時間逸出子句：  
  
         **{ ts'**yyyy**-***mm***-***dd**hh***:***mm***:***ss*[**.***fff*] **'}** 例如： **{ ts'**1998**-**09**-**24 10**:**02**:**20**' }**  
  
         **{ d'** *yyyy* **-** *mm* **-** *dd* **'}** such as: **{ d'**1998**-**09**-**24**'}**  
  
         **{ t'** *hh* **:** *mm* **:** *ss* **'}** such as: **{ t'**10:02:20**'}**  
  
    -   使用其他 API 或 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼、預存程序和觸發程序的應用程式，應該使用未分隔的數值字串。 例如 *yyyymmdd* 為 19980924。  
  
    -   使用其他 API 的應用程式，或 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼、預存程序和觸發程序，都應該針對 **time**、 **date**、 **smalldate**、 **datetime**、 **datetime2**，和 **datetimeoffset** 資料類型以及字元字串資料類型之間的所有轉換使用明確樣式參數的 CONVERT 陳述式。 例如，下列陳述式在所有日期格式連接設定下的解譯都是一樣的：  
  
        ```  
        SELECT *  
        FROM AdventureWorks2012.Sales.SalesOrderHeader  
        WHERE OrderDate = CONVERT(DATETIME, '20060719', 101)  
        ```  
  
         如需詳細資訊，請參閱 [CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)。  
  
  


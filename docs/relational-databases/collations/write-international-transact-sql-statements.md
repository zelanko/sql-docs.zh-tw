---
title: 撰寫國際通用的 Transact-SQL 陳述式 | Microsoft Docs
ms.custom: ''
ms.date: 04/24/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- writing international statements
- Transact-SQL international considerations
- international considerations [SQL Server], Transact-SQL
- Database Engine international considerations [SQL Server], Transact-SQL
- statements [SQL Server], international
- database international considerations [SQL Server], Transact-SQL
- dates [SQL Server], international considerations
ms.assetid: f0b10fee-27f7-45fe-aece-ccc3f63bdcdb
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 20e587aeb7c0ed34762bf1f90488a06cafc0ec93
ms.sourcegitcommit: 0a4879dad09c6c42ad1ff717e4512cfea46820e9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/27/2019
ms.locfileid: "67412991"
---
# <a name="write-international-transact-sql-statements"></a>撰寫國際通用的 Transact-SQL 陳述式
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  如果遵循下列的指導方針，使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的資料庫與資料庫應用程式將更能從一個語言移植至另一個語言，或可支援多種語言：  

-   從 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 開始，使用：
    -   **char**、**varchar** 及 **varchar(max)** 資料類型 (使用啟用 [UTF-8](../../relational-databases/collations/collation-and-unicode-support.md#utf8) 的定序)。
    -   **char**、**varchar** 及 **varchar(max)** 資料類型 (使用啟用[增補字元](../../relational-databases/collations/collation-and-unicode-support.md#Supplementary_Characters)的定序)。      

    這可避免字碼頁轉換問題。 如需其它考量事項，請參閱 [UTF-8 和 UTF-16 間的儲存差異](../../relational-databases/collations/collation-and-unicode-support.md#storage_differences)。  

-   最多到 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]，使用 **nchar**、**nvarchar** 及 **nvarchar(max)** 來取代所有使用的 **char**、**varchar** 及 **varchar(max)** 資料類型。 這可避免字碼頁轉換問題。 如需詳細資訊，請參閱 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)。 
    > [!IMPORTANT]
    > **text** 資料類型已淘汰，不應用於新的開發工作。 計劃將 **text** 資料轉換為 **varchar(max)** 。
  
-   您在執行月份和週中日的比較和運算時，請使用數值的日期部分，而不要使用名稱字串。 不同的語言設定會傳回不同的月份和週中日名稱。 例如，語言設定為「英文 (美國)」時，`DATENAME(MONTH,GETDATE())` 會傳回 `May`；當語言設定為「德文」時，會傳回 `Mai`；而當語言設定為「法文」時，會傳回 `mai`。 請改用如 [DATEPART](../../t-sql/functions/datepart-transact-sql.md) 的函式，使用數字月份而非名稱。 當您要將結果集顯示給使用者時，請使用 DATEPART 名稱，因為日期名稱通常比數值表示法來得有意義。 但是，不要根據特定語言的顯示名稱來撰寫任何程式碼邏輯。  
  
-   當您在比較或輸入至 INSERT 或 UPDATE 陳述式中指定日期時，請使用所有語言設定都作相同解譯的常數：  
  
    -   ADO、OLE DB 和 ODBC 應用程式應該使用以下形式的 ODBC 時間戳記、日期和時間逸出子句：  
  
         **{ ts'** _yyyy_ **-** _mm_ **-** _dd_ _hh_ **:** _mm_ **:** _ss_ [ **.** _fff_] **'}** 例如： **{ ts'1998-09-24 10:02:20'}**  
  
         **{ d'** _yyyy_ **-** _mm_ **-** _dd_ **'}** 例如： **{ d'1998-09-24'}**
  
         **{ t'** _hh_ **:** _mm_ **:** _ss_ **'}** 例如： **{ t'10:02:20'}**  
  
    -   使用其他 API 或 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼、預存程序和觸發程序的應用程式，應該使用未分隔的數值字串。 例如 *yyyymmdd* 為 19980924。  
  
    -   使用其他 API 的應用程式，或 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼、預存程序及觸發程序，都應該針對 **time**、**date**、**smalldate**、**datetime**、**datetime2** 和 **datetimeoffset** 資料類型與字元字串資料類型之間的所有轉換，使用具有明確樣式參數的 [CONVERT](../../t-sql/functions/cast-and-convert-transact-sql.md) 陳述式。 例如，下列陳述式在所有日期格式連接設定下的解譯都是一樣的：  
  
        ```sql  
        SELECT *  
        FROM AdventureWorks2012.Sales.SalesOrderHeader  
        WHERE OrderDate = CONVERT(DATETIME, '20060719', 101)  
        ```  
  
## <a name="see-also"></a>另請參閱
[CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)     
[DATEPART &#40;Transact-SQL&#41;](../../t-sql/functions/datepart-transact-sql.md)        
[定序與 Unicode 支援](../../relational-databases/collations/collation-and-unicode-support.md)      

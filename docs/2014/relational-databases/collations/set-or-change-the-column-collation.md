---
title: 設定或變更資料行定序 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- tempdb database [SQL Server], collations
- collations [SQL Server], column
ms.assetid: d7a9638b-717c-4680-9b98-8849081e08be
caps.latest.revision: 29
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 3de84f26e894f00760a45d5e65769c0db8d4b009
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36022885"
---
# <a name="set-or-change-the-column-collation"></a>設定或變更資料行定序
  您可以覆寫的資料庫定序`char`， `varchar`， `text`， `nchar`， `nvarchar`，和`ntext`資料所指定資料表中特定資料行不同的定序，並使用下列其中之一：  
  
-   [CREATE TABLE](/sql/t-sql/statements/create-table-transact-sql) 和 [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql)的 COLLATE 子句。 例如：  
  
    ```  
    CREATE TABLE dbo.MyTable  
      (PrimaryKey   int PRIMARY KEY,  
       CharCol      varchar(10) COLLATE French_CI_AS NOT NULL  
      );  
    GO  
    ALTER TABLE dbo.MyTable ALTER COLUMN CharCol  
                varchar(10)COLLATE Latin1_General_CI_AS NOT NULL;  
    GO  
    ```  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的 COLLATE 子句。 如需詳細資訊，請參閱 [定序與 Unicode 支援](collation-and-unicode-support.md)。  
  
-   使用`Column.Collation`屬性[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]管理物件 (SMO)。  
  
 如果目前下列任何一個項目參考資料行定序的話，就無法變更其定序：  
  
-   計算資料行  
  
-   索引  
  
-   散發統計資料，不論是自動產生或由 CREATE STATISTICS 陳述式產生  
  
-   CHECK 條件約束  
  
-   FOREIGN KEY 條件約束  
  
 當您使用 **tempdb**時， [COLLATE](/sql/t-sql/statements/collations) 子句會包含 *database_default* 選項，將暫存資料表中的資料行指定為使用連線的目前使用者資料庫預設定序，而非 **tempdb**的定序。  
  
## <a name="collations-and-text-columns"></a>定序與 text 資料行  
 您可以插入或更新中的值`text`其定序是資料庫的預設定序字碼頁不同的資料行。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以隱含方式將該值轉換為資料行定序。  
  
## <a name="collations-and-tempdb"></a>定序與 tempdb  
 **tempdb** 資料庫在每次 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 啟動時建置，且預設定序與 **model** 資料庫相同。 通常與執行個體的預設定序相同。 如果建立使用者資料庫，並指定與 **model**不同的預設定序，使用者資料庫的預設定序就會與 **tempdb**不同。 所有暫存預存程序或暫存資料表會在 **tempdb**中建立及儲存。 這表示暫存資料表中所有隱含的資料行，與暫存預存程序中所有可強迫的常數、變數與參數，都會與建在永久資料表和預存程序中的同等物件具有不同的定序。  
  
 這將造成使用者自訂資料庫與系統資料庫物件之間的定序不相符。 例如， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體使用 Latin1_General_CS_AS 定序，而您執行下列陳述式：  
  
```  
CREATE DATABASE TestDB COLLATE Estonian_CS_AS;  
USE TestDB;  
CREATE TABLE TestPermTab (PrimaryKey int PRIMARY KEY, Col1 nchar );  
```  
  
 在此系統中， **tempdb** 資料庫使用 Latin1_General_CS_AS 定序與字碼頁 1252，而 `TestDB` 和 `TestPermTab.Col1` 使用 `Estonian_CS_AS` 定序與字碼頁 1257。 例如：  
  
```  
USE TestDB;  
GO  
-- Create a temporary table with the same column declarations  
-- as TestPermTab  
CREATE TABLE #TestTempTab (PrimaryKey int PRIMARY KEY, Col1 nchar );  
INSERT INTO #TestTempTab  
         SELECT * FROM TestPermTab;  
GO  
```  
  
 承上例， **tempdb** 資料庫使用 Latin1_General_CS_AS 定序，而 `TestDB` 和 `TestTab.Col1` 則使用 `Estonian_CS_AS` 定序。 例如：  
  
```  
SELECT * FROM TestPermTab AS a INNER JOIN #TestTempTab on a.Col1 = #TestTempTab.Col1;  
```  
  
 因為 **tempdb** 使用預設伺服器定序，而 `TestPermTab.Col1` 使用不同的定序，所以 SQL Server 會傳回此錯誤訊息：「無法解析等於作業中，'Latin1_General_CI_AS_KS_WS' 與 'Estonian_CS_AS' 之間的定序衝突」。  
  
 為避免此錯誤，您可以使用以下任一種替代方法：  
  
-   指定暫存資料表的資料行使用使用者資料庫的預設定序，而不使用 **tempdb**的預設定序。 這使得暫存資料表可配合多個資料庫中格式類似的資料表 (如果系統有這樣的需求)。  
  
    ```  
    CREATE TABLE #TestTempTab  
       (PrimaryKey int PRIMARY KEY,  
        Col1 nchar COLLATE database_default  
       );  
    ```  
  
-   為 `#TestTempTab` 資料行指定正確的定序：  
  
    ```  
    CREATE TABLE #TestTempTab  
       (PrimaryKey int PRIMARY KEY,  
        Col1 nchar COLLATE Estonian_CS_AS  
       );  
    ```  
  
## <a name="see-also"></a>另請參閱  
 [設定或變更伺服器定序](set-or-change-the-server-collation.md)   
 [設定或變更資料庫定序](set-or-change-the-database-collation.md)   
 [定序與 Unicode 支援](collation-and-unicode-support.md)  
  
  

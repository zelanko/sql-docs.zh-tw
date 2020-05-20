---
title: 設定或變更資料行定序 | Microsoft Docs
ms.custom: ''
ms.date: 12/05/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- tempdb database [SQL Server], collations
- collations [SQL Server], column
ms.assetid: d7a9638b-717c-4680-9b98-8849081e08be
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0880ce366c2db15f7e751c9493bebf5f97d4240a
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "74908713"
---
# <a name="set-or-change-the-column-collation"></a>設定或變更資料行定序
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  您可以透過為資料表中特定資料行指定不同的定序並使用下列其中一種方法，覆寫 **char**、 **varchar**、 **text**、 **nchar**、 **nvarchar**和 **ntext** 資料的資料庫定序：  
  
-   [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) 和 [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) 的 COLLATE 子句，如以下範例所示。 

    -   **就地轉換。** 請考慮以下定義的其中一個現有資料表：

        ```sql
        -- NVARCHAR column is encoded in UTF-16 because a supplementary character enabled collation is used
        CREATE TABLE dbo.MyTable (CharCol NVARCHAR(50) COLLATE Latin1_General_100_CI_AI_SC);

        -- VARCHAR column is encoded the Latin code page and therefore is not Unicode capable
        CREATE TABLE dbo.MyTable (CharCol VARCHAR(50) COLLATE Latin1_General_100_CI_AI);
        ```

        若要將資料行就地轉換成使用 UTF-8，請執行 `ALTER COLUMN` 陳述式，以設定所需的資料類型和支援 UTF-8 的定序：

        ```sql 
        ALTER TABLE dbo.MyTable 
        ALTER COLUMN CharCol VARCHAR(50) COLLATE Latin1_General_100_CI_AI_SC_UTF8
        ```

        此方法很容易實作，不過它可能是封鎖作業，會成為大型資料表和忙碌應用程式的問題。

    -   **複製並取代。** 請考慮以下定義的其中一個現有資料表：

        ```sql
        -- NVARCHAR column is encoded in UTF-16 because a supplementary character enabled collation is used
        CREATE TABLE dbo.MyTable (CharCol NVARCHAR(50) COLLATE Latin1_General_100_CI_AI_SC);
        GO

        -- VARCHAR column is encoded using the Latin code page and therefore is not Unicode capable
        CREATE TABLE dbo.MyTable (CharCol VARCHAR(50) COLLATE Latin1_General_100_CI_AI);
        GO
        ```

        為了將資料行轉換成使用 UTF-8，範例將資料複製到新資料表，其中目標資料行已是所需的資料類型和支援 UTF-8 的定序，然後取代舊資料表：

        ```sql
        CREATE TABLE dbo.MyTableNew (CharCol VARCHAR(50) COLLATE Latin1_General_100_CI_AI_SC_UTF8);
        GO
        INSERT INTO dbo.MyTableNew 
        SELECT * FROM dbo.MyTable;
        GO
        DROP TABLE dbo.MyTable;
        GO
        EXEC sp_rename 'dbo.MyTableNew', 'dbo.MyTable’;
        GO
        ```

        此方法比就地轉換更快，但是使用許多相依性 (FK、PK、觸發程序、DF) 來處理複雜結構描述，而且同步資料表結尾 (如果資料庫正在使用中) 需要更多的規劃。
        
    如需詳細資訊，請參閱 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)。
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]第 1 課：建立 Windows Azure 儲存體物件[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 如需詳細資訊，請參閱[修改資料行 (資料庫引擎)](../../relational-databases/tables/modify-columns-database-engine.md#SSMSProcedure)。  
  
-   使用 **管理物件 (SMO) 中的** Column.Collation [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 屬性。  
  
 如果目前下列任何一個項目參考資料行定序的話，就無法變更其定序：  
  
-   計算資料行  
-   索引  
-   散發統計資料，不論是自動產生或由 `CREATE STATISTICS` 陳述式產生  
-   CHECK 條件約束  
-   FOREIGN KEY 條件約束  
  
 當您使用 **tempdb**時， [COLLATE](~/t-sql/statements/collations.md) 子句會包含 *database_default* 選項，將暫存資料表中的資料行指定為使用連線的目前使用者資料庫預設定序，而非 **tempdb**的定序。  
  
## <a name="collations-and-text-columns"></a>定序與 text 資料行  
 您可以插入或更新 **text** 資料行的值，該資料行定序與資料庫預設定序的字碼頁不同。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以隱含方式將該值轉換為資料行定序。  
  
## <a name="collations-and-tempdb"></a>定序與 tempdb  
 **tempdb** 資料庫在每次 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 啟動時建置，且預設定序與 **model** 資料庫相同。 通常與執行個體的預設定序相同。 如果建立使用者資料庫，並指定與 **model**不同的預設定序，使用者資料庫的預設定序就會與 **tempdb**不同。 所有暫存預存程序或暫存資料表會在 **tempdb**中建立及儲存。 這表示暫存資料表中所有隱含的資料行，與暫存預存程序中所有可強迫的常數、變數與參數，都會與建在永久資料表和預存程序中的同等物件具有不同的定序。  
  
 這將造成使用者自訂資料庫與系統資料庫物件之間的定序不相符。 例如， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體使用 Latin1_General_CS_AS 定序，而您執行下列陳述式：  
  
```sql  
CREATE DATABASE TestDB COLLATE Estonian_CS_AS;  
USE TestDB;  
CREATE TABLE TestPermTab (PrimaryKey int PRIMARY KEY, Col1 nchar );  
```  
  
 在此系統中， **tempdb** 資料庫使用 Latin1_General_CS_AS 定序與字碼頁 1252，而 `TestDB` 和 `TestPermTab.Col1` 使用 `Estonian_CS_AS` 定序與字碼頁 1257。 例如：  
  
```sql  
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
  
```sql  
SELECT * FROM TestPermTab AS a INNER JOIN #TestTempTab on a.Col1 = #TestTempTab.Col1;  
```  
  
 因為 **tempdb** 使用預設伺服器定序，而 `TestPermTab.Col1` 使用不同的定序，所以 SQL Server 會傳回此錯誤訊息：「無法解析等於作業中，'Latin1_General_CI_AS_KS_WS' 與 'Estonian_CS_AS' 之間的定序衝突」。  
  
 為避免此錯誤，您可以使用以下任一種替代方法：  
  
-   指定暫存資料表的資料行使用使用者資料庫的預設定序，而不使用 **tempdb**的預設定序。 這使得暫存資料表可配合多個資料庫中格式類似的資料表 (如果系統有這樣的需求)。  
  
    ```sql  
    CREATE TABLE #TestTempTab  
       (PrimaryKey int PRIMARY KEY,  
        Col1 nchar COLLATE database_default  
       );  
    ```  
  
-   為 `#TestTempTab` 資料行指定正確的定序：  
  
    ```sql  
    CREATE TABLE #TestTempTab  
       (PrimaryKey int PRIMARY KEY,  
        Col1 nchar COLLATE Estonian_CS_AS  
       );  
    ```  
  
## <a name="see-also"></a>另請參閱  
 [設定或變更伺服器定序](../../relational-databases/collations/set-or-change-the-server-collation.md)   
 [設定或變更資料庫定序](../../relational-databases/collations/set-or-change-the-database-collation.md)   
 [定序與 Unicode 支援](../../relational-databases/collations/collation-and-unicode-support.md)  
  
  

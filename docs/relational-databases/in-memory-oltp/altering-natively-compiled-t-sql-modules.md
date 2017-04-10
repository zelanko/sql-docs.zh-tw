---
title: "更改原生編譯的 T-SQL 模組 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine-imoltp"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 010318a0-6807-47c3-8ecc-bb7cb60513f0
caps.latest.revision: 7
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 7
---
# 更改原生編譯的 T-SQL 模組
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  在 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] (和更新版本) 和 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 中，您可以使用 ALTER 陳述式在原生編譯預存程序以及純量 UDF 和觸發程序等其他原生編譯的 T-SQL 模組上執行 ALTER 作業。  
  
 在原生編譯 T-SQL 模組上執行 ALTER 時，模組會使用新的定義重新編譯。 進行重新編譯時，舊版的模組仍可繼續執行。 編譯完成之後，即會清空模組執行，並安裝新版的程序。 當您改變原生編譯的 T-SQL 模組時，可以修改下列選項。  
  
-   參數  
  
-   EXECUTE AS  
  
-   TRANSACTION ISOLATION LEVEL  
  
-   LANGUAGE  
  
-   DATEFIRST  
  
-   DATEFORMAT  
  
-   DELAYED_DURABILITY  
  
> [!NOTE]  
>  原生編譯 T-SQL 模組無法轉換成非原生編譯的模組。 非原生編譯 T-SQL 模組無法轉換成原生編譯的模組。  
  
 如需 ALTER PROCEDURE 功能和語法的詳細資訊，請參閱 [ALTER PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-procedure-transact-sql.md)。  
  
 您可以在原生編譯 T-SQL 模組上執行 sp_recompile，下次執行時就會重新編譯組。  
  
## 範例  
 下例會建立記憶體最佳化的資料表 (T1)，以及選取所有 T1 資料行的原生編譯預存程序 (SP1)。 然後，更改 SP1 以移除 EXECUTE AS 子句、變更 LANGUAGE，從 T1 只選取有一個資料行 (C1)。  
  
```  
CREATE TABLE [dbo].[T1]  
(  
[c1] [int] NOT NULL,  
[c2] [float] NOT NULL,  
CONSTRAINT [PK_T1] PRIMARY KEY NONCLUSTERED ([c1])  
)WITH ( MEMORY_OPTIMIZED = ON , DURABILITY = SCHEMA_AND_DATA )  
GO  
  
CREATE PROCEDURE [dbo].[usp_1]  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH  
(  
 TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english'  
)  
 SELECT c1, c2 from dbo.T1  
END  
GO  
  
ALTER PROCEDURE [dbo].[usp_1]  
WITH NATIVE_COMPILATION, SCHEMABINDING  
AS BEGIN ATOMIC WITH  
(  
 TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'Dutch'  
)  
 SELECT c1 from dbo.T1  
END  
GO  
  
```  
  
  
---
title: 從預存程序建立及存取 TempDb 資料表
ms.custom: seo-dt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 12be8011-b76c-45c1-8f55-7f46e0e374e9
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f4ae543590e5985904e44235da89069c06c649ee
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "74412716"
---
# <a name="create-and-access-tables-in-tempdb-from-stored-procedures"></a>從預存程序建立及存取 TempDB 中的資料表
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  不支援從原生編譯預存程序建立及存取 TempDB 中的資料表。 請改用 DURABILITY=SCHEMA_ONLY 的記憶體最佳化資料表，或改用資料表類型和資料表變數。 

如需暫存資料表和資料表變數案例之記憶體最佳化的詳細資訊，請參閱 [使用記憶體最佳化加快暫存資料表與資料表變數的速度](../../relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization.md)。
  
  下列範例示範如何使用 **dbo.OrderQuantityByProduct** 類型的 **\@OrderQuantityByProduct** 資料表變數取代暫存資料表 (其具有 id、ProductID、Quantity 這三個資料行)：  
  
```sql  
CREATE TYPE dbo.OrderQuantityByProduct   
  AS TABLE   
   (id INT NOT NULL PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT=100000),   
    ProductID INT NOT NULL,   
    Quantity INT NOT NULL) WITH (MEMORY_OPTIMIZED=ON)  
GO  
CREATE PROCEDURE dbo.usp_OrderQuantityByProduct   
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH   
(  
    TRANSACTION ISOLATION LEVEL = SNAPSHOT,  
    LANGUAGE = N'ENGLISH'  
)  
  -- declare table variables for the list of orders   
  DECLARE @OrderQuantityByProduct dbo.OrderQuantityByProduct  
  
  -- populate input  
  INSERT @OrderQuantityByProduct SELECT ProductID, Quantity FROM dbo.[Order Details]  
  end  
```  
  
## <a name="see-also"></a>另請參閱  
 [原生編譯預存程序的移轉問題](../../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md)   
 [記憶體中的 OLTP 不支援 Transact-SQL 建構](../../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md)  
  
  

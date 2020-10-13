---
title: 原生編譯 Advisor | Microsoft Docs
description: 了解如何使用原生編譯建議程式，將解譯的預存程序遷移至原生編譯，作為移轉至記憶體內部 OLTP 的一部分。
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
f1_keywords:
- sql13.swb.nativecompilationwizard.f1
- swb.nativecompilationwizard.f1
ms.assetid: d3898a47-2985-4a08-bc70-fd8331a01b7b
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: efbd90e43c4f2bf7863106330b59f436c31b6238
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/09/2020
ms.locfileid: "91868537"
---
# <a name="native-compilation-advisor"></a>原生編譯 Advisor
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  交易效能分析報表會通知您，資料庫中哪些解譯的預存程序將能因匯出使用原生編譯而受益。 如需詳細資訊，請參閱 [判斷是否應將資料表或預存程序匯出至記憶體中 OLTP](../../relational-databases/in-memory-oltp/determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md)。  
  
 識別您要匯出使用原生編譯的預存程序之後，即可使用原生編譯建議程式 (NCA) 協助您將解譯的預存程序移轉到原生編譯。 如需原生編譯的預存程序的詳細資訊，請參閱 [原生編譯的預存程序](./a-guide-to-query-processing-for-memory-optimized-tables.md)。  
  
 在指定解譯預存程序中，NCA 可讓您識別原生模組中不支援的所有功能。 NCA 提供解決方法或解決方案的文件連結。  
  
 如需移轉方法的資訊，請參閱 [In-Memory OLTP - 一般工作負載模式和移轉考量](/previous-versions/dn673538(v=msdn.10))。  
  
## <a name="walkthrough-using-the-native-compilation-advisor"></a>使用原生編譯 Advisor 的逐步解說  
 在 [物件總管] 中，以滑鼠右鍵按一下您想要轉換的預存程序，然後選取 [原生編譯 Advisor]。 隨即顯示 [預存程序原生編譯 Advisor] 的歡迎頁面。 選取 [下一步] 以繼續操作。  
  
### <a name="stored-procedure-validation"></a>預存程序驗證  
 此頁面將會回報預存程序是否使用任何與原生編譯不相容的建構。 您可以按 [下一步] 查看詳細資料。 如果有與原生編譯不相容的建構，您可以按 [下一步] 查看詳細資料。  
  
### <a name="stored-procedure-validation-result"></a>預存程序驗證結果  
 如果有與原生編譯不相容的建構，[預存程序驗證結果] 頁面會顯示詳細資料。 您可以產生報表 (按一下 [產生報表])、結束 [原生編譯 Advisor]，並更新您的程式碼，使其與原生編譯相容。  
  
## <a name="code-sample"></a>程式碼範例  
 下列範例顯示解譯的預存程序及原生編譯的「對等」預存程序。 該範例假設目錄名為 c:\data。  
  
> [!NOTE]  
>  像往常一樣， **FILEGROUP** 元素和 **USE** mydatabase 陳述式，會套用至 Microsoft SQL Server，但是不會套用至 Azure SQL Database。  
  
```sql  
CREATE DATABASE Demo  
ON  
PRIMARY(NAME = [Demo_data],  
FILENAME = 'C:\DATA\Demo_data.mdf', size=500MB)  
, FILEGROUP [Demo_fg] CONTAINS MEMORY_OPTIMIZED_DATA(  
NAME = [Demo_dir],  
FILENAME = 'C:\DATA\Demo_dir')  
LOG ON (name = [Demo_log], Filename='C:\DATA\Demo_log.ldf', size=500MB)  
COLLATE Latin1_General_100_BIN2;  
go  
  
USE Demo;  
go  
  
CREATE TABLE [dbo].[SalesOrders]  
(  
     [order_id] [int] NOT NULL,  
     [order_date] [datetime] NOT NULL,  
     [order_status] [tinyint] NOT NULL  
     CONSTRAINT [PK_SalesOrders] PRIMARY KEY NONCLUSTERED HASH   
(  
     [order_id]  
) WITH ( BUCKET_COUNT = 2097152)  
) WITH ( MEMORY_OPTIMIZED = ON )  
go  
  
-- Interpreted.  
CREATE PROCEDURE [dbo].[InsertOrder] @id INT, @date DATETIME2, @status TINYINT  
AS   
BEGIN   
  INSERT dbo.SalesOrders VALUES (@id, @date, @status);  
END  
go  
  
-- Natively Compiled.  
CREATE PROCEDURE [dbo].[InsertOrderXTP]  
      @id INT, @date DATETIME2, @status TINYINT  
  WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS   
BEGIN ATOMIC WITH   
     (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english'  
     )  
  INSERT dbo.SalesOrders VALUES (@id, @date, @status);  
END  
go  
  
SELECT * from SalesOrders;  
go  
  
EXECUTE dbo.InsertOrder @id= 10, @date = '1956-01-01 12:00:00', @status = 1;  
EXECUTE dbo.InsertOrderXTP @id= 11, @date = '1956-01-01 12:01:00', @status = 2;  
  
SELECT * from SalesOrders;  
```  
  
## <a name="see-also"></a>另請參閱  
 [移轉至 In-Memory OLTP](./plan-your-adoption-of-in-memory-oltp-features-in-sql-server.md)   
 [使用記憶體最佳化資料表的需求](../../relational-databases/in-memory-oltp/requirements-for-using-memory-optimized-tables.md)  
  

---
title: 原生編譯 Advisor | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
f1_keywords:
- sql12.swb.nativecompilationwizard.f1
- swb.nativecompilationwizard.f1
ms.assetid: d3898a47-2985-4a08-bc70-fd8331a01b7b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5174b5c859fa76ceeccdb99b7a46f510fd62d923
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63072744"
---
# <a name="native-compilation-advisor"></a>原生編譯 Advisor
  交易效能報告工具（請參閱[判斷是否應將資料表或預存程式移植到記憶體內部 OLTP](determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md)）會通知您，如果您的資料庫中有哪些已轉譯的預存程式會在移植使用原生編譯時受益。 識別您要匯出使用原生編譯的預存程序之後，即可使用原生編譯 Advisor 協助您將解譯的預存程序移轉到原生編譯。 如需原生編譯的預存程序的詳細資訊，請參閱 [原生編譯的預存程序](natively-compiled-stored-procedures.md)。  
  
 開始時，請先連接至執行個體，其中包含解譯的預存程序。 您可以連接到 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 或 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 執行個體。 不過，如果您想要使用 Advisor 執行移轉作業，則必須連接到已啟用 In-Memory OLTP 功能的 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 執行個體。 如需有關記憶體中 OLTP 需求的詳細資訊，請參閱＜ [Requirements for Using Memory-Optimized Tables](memory-optimized-tables.md)＞。  
  
 如需移轉方法的資訊，請參閱 [In-Memory OLTP - 一般工作負載模式和移轉考量](https://msdn.microsoft.com/library/dn673538.aspx)。  
  
## <a name="walkthrough-using-the-native-compilation-advisor"></a>使用原生編譯 Advisor 的逐步解說  
 在 [物件總管]**** 中，以滑鼠右鍵按一下您想要轉換的預存程序，然後選取 [原生編譯 Advisor]****。 隨即顯示 [預存程序原生編譯 Advisor]**** 的歡迎頁面。 按 **[下一步]**，繼續進行。  
  
### <a name="stored-procedure-validation"></a>預存程序驗證  
 此頁面將會回報預存程序是否使用任何與原生編譯不相容的建構。 您可以按 [下一步]**** 查看詳細資料。 如果有與原生編譯不相容的建構，您可以按 [下一步]**** 查看詳細資料。  
  
### <a name="stored-procedure-validation-result"></a>預存程序驗證結果  
 如果有與原生編譯不相容的建構，[預存程序驗證結果]**** 頁面會顯示詳細資料。 您可以產生報表 (按一下 [產生報表]****)、結束 [原生編譯 Advisor]****，並更新您的程式碼，使其與原生編譯相容。  
  
## <a name="code-sample"></a>程式碼範例  
 下列範例顯示解譯的預存程序及原生編譯的對等預存程序。 該範例假設目錄名為 c:\data。  
  
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
GO  
USE Demo;  
GO  
  
CREATE TABLE [dbo].[SalesOrders]  
(  
     [order_id] [int] NOT NULL,  
     [order_date] [datetime] NOT NULL,  
     [order_status] [tinyint] NOT NULL  
  
CONSTRAINT [PK_SalesOrders] PRIMARY KEY NONCLUSTERED HASH   
(  
     [order_id]  
)WITH ( BUCKET_COUNT = 2097152)  
)WITH ( MEMORY_OPTIMIZED = ON )  
  
go  
  
CREATE PROCEDURE [dbo].[InsertOrder] @id INT, @date DATETIME2, @status TINYINT  
AS   
BEGIN   
  
  INSERT dbo.SalesOrders VALUES (@id, @date, @status)  
  
END  
  
go  
  
CREATE PROCEDURE [dbo].[InsertOrderXTP] @id INT, @date DATETIME2, @status TINYINT  
  WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS   
BEGIN ATOMIC WITH   
(    TRANSACTION ISOLATION LEVEL = SNAPSHOT,  
     LANGUAGE = N'us_english')  
  
  INSERT dbo.SalesOrders VALUES (@id, @date, @status)  
  
END  
go  
  
select * from SalesOrders  
go  
exec dbo.InsertOrder @id= 10, @date = '1956-01-01 12:00:00', @status = 1 ;  
exec dbo.InsertOrderXTP @id= 11, @date = '1956-01-01 12:01:00', @status = 2 ;  
select * from SalesOrders  
```  
  
## <a name="see-also"></a>另請參閱  
 [移轉至 In-Memory OLTP](migrating-to-in-memory-oltp.md)  
  
  

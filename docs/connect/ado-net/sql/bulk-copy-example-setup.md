---
title: 大量複製範例設定
description: 描述大量複製範例中所使用的資料表，並提供可用來在 AdventureWorks 資料庫中建立資料表的 SQL 指令碼。
ms.date: 09/30/2019
dev_langs:
- sql
ms.assetid: d4dde6ac-b8b6-4593-965a-635c8fb2dadb
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: 601a761f3ef63b4ae2394633d82f27471719e34c
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80928921"
---
# <a name="bulk-copy-example-setup"></a>大量複製範例設定

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

<xref:Microsoft.Data.SqlClient.SqlBulkCopy> 類別只能用來將資料寫入到 SQL Server 資料表。 本主題中所顯示的程式碼範例會使用 SQL Server 範例資料庫 **AdventureWorks**。 若要避免變更現有資料表的程式碼範例，請將資料寫入您必須先建立的資料表。  
  
**BulkCopyDemoMatchingColumns** 和 **BulkCopyDemoDifferentColumns** 資料表都會以 **AdventureWorks** **Production.Products** 資料表為基礎。 在使用這些資料表的程式碼範例中，會將來自 **Production.Products** 資料表的資料新增至其中一個範例資料表。 當此範例說明如何將來源資料的資料行對應至目的地資料表時，會使用 **BulkCopyDemoDifferentColumns** 資料表；**BulkCopyDemoMatchingColumns** 也適用於大部分其他範例。  
  
幾個程式碼範例示範如何使用一個 <xref:Microsoft.Data.SqlClient.SqlBulkCopy> 類別來寫入多個資料表。 在這些範例中，**BulkCopyDemoOrderHeader** 和 **BulkCopyDemoOrderDetail** 資料表用來當作目的地資料表。 這些資料表以 **AdventureWorks** 中的 **Sales.SalesOrderHeader** 和 **Sales.SalesOrderDetail** 資料表為基礎。  
  
> [!NOTE]
>  **SqlBulkCopy** 程式碼範例只是為了示範使用 **SqlBulkCopy** 的語法而提供。 如果來源和目的地資料表位於相同的 SQL Server 執行個體，則使用 Transact-SQL `INSERT … SELECT` 陳述式來複製資料會更方便且快速。  
  
## <a name="table-setup"></a>資料表設定  
若要建立程式碼範例正確執行所需的資料表，您必須在 SQL Server 資料庫中執行下列 Transact-SQL 陳述式。  
  
```sql
USE AdventureWorks  
  
IF EXISTS (SELECT * FROM dbo.sysobjects   
 WHERE id = object_id(N'[dbo].[BulkCopyDemoMatchingColumns]')  
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoMatchingColumns]  
  
CREATE TABLE [dbo].[BulkCopyDemoMatchingColumns]([ProductID] [int] IDENTITY(1,1) NOT NULL,  
    [Name] [nvarchar](50) NOT NULL,  
    [ProductNumber] [nvarchar](25) NOT NULL,  
 CONSTRAINT [PK_ProductID] PRIMARY KEY CLUSTERED  
(  
    [ProductID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
IF EXISTS (SELECT * FROM dbo.sysobjects   
 WHERE id = object_id(N'[dbo].[BulkCopyDemoDifferentColumns]')  
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoDifferentColumns]  
  
CREATE TABLE [dbo].[BulkCopyDemoDifferentColumns]([ProdID] [int] IDENTITY(1,1) NOT NULL,  
    [ProdNum] [nvarchar](25) NOT NULL,  
    [ProdName] [nvarchar](50) NOT NULL,  
 CONSTRAINT [PK_ProdID] PRIMARY KEY CLUSTERED  
(  
    [ProdID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
IF EXISTS (SELECT * FROM dbo.sysobjects   
 WHERE id = object_id(N'[dbo].[BulkCopyDemoOrderHeader]')  
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoOrderHeader]  
  
CREATE TABLE [dbo].[BulkCopyDemoOrderHeader]([SalesOrderID] [int] IDENTITY(1,1) NOT NULL,  
    [OrderDate] [datetime] NOT NULL,  
    [AccountNumber] [nvarchar](15) NULL,  
 CONSTRAINT [PK_SalesOrderID] PRIMARY KEY CLUSTERED  
(  
    [SalesOrderID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
IF EXISTS (SELECT * FROM dbo.sysobjects   
 WHERE id = object_id(N'[dbo].[BulkCopyDemoOrderDetail]')  
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoOrderDetail]  
  
CREATE TABLE [dbo].[BulkCopyDemoOrderDetail]([SalesOrderID] [int] NOT NULL,  
    [SalesOrderDetailID] [int] NOT NULL,  
    [OrderQty] [smallint] NOT NULL,  
    [ProductID] [int] NOT NULL,  
    [UnitPrice] [money] NOT NULL,  
 CONSTRAINT [PK_LineNumber] PRIMARY KEY CLUSTERED  
(  
    [SalesOrderID] ASC,  
    [SalesOrderDetailID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
```  
  
## <a name="next-steps"></a>後續步驟
- [SQL Server 中的大量複製作業](bulk-copy-operations-sql-server.md)

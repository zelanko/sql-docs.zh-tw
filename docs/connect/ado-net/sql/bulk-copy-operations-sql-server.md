---
title: SQL Server 中的大量複製作業
description: 說明 .NET Data Provider for SQL Server 的大量複製功能。
ms.date: 09/30/2019
ms.assetid: 83a7a0d2-8018-4354-97b9-0b1d99f8342b
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: d038b0a67923d7c475011b8f3d141f7d64358f61
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "75247864"
---
# <a name="bulk-copy-operations-in-sql-server"></a>SQL Server 中的大量複製作業

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下載 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Microsoft SQL Server 包含名為 **bcp** 的常用命令列公用程式，用於將大型檔案快速大量複製到 SQL Server 資料庫中的資料表或檢視。 <xref:Microsoft.Data.SqlClient.SqlBulkCopy> 類別可讓您撰寫受控程式碼解決方案來提供類似功能。 還有其他方法可以將資料載入 SQL Server 資料表 (例如 INSERT 陳述式)，但 <xref:Microsoft.Data.SqlClient.SqlBulkCopy> 提供顯著超越其他方法的效能優勢。  
  
使用 <xref:Microsoft.Data.SqlClient.SqlBulkCopy> 類別，您可以執行：  
  
- 單一大量複製作業  
  
- 多項大量複製作業  
  
- 交易內的大量複製作業  
  
> [!NOTE]
>  當使用 .NET Framework 1.1 版或更早版本 (不支援 <xref:Microsoft.Data.SqlClient.SqlBulkCopy> 類別) 時，您可使用 <xref:Microsoft.Data.SqlClient.SqlCommand> 物件執行 SQL Server Transact-SQL **BULK INSERT** 陳述式。  
  
## <a name="in-this-section"></a>本節內容  
[大量複製範例設定](bulk-copy-example-setup.md)  
描述大量複製範例中所使用的資料表，並提供可用來在 AdventureWorks 資料庫中建立資料表的 SQL 指令碼。  
  
[單一大量複製作業](single-bulk-copy-operations.md)  
描述如何使用 <xref:Microsoft.Data.SqlClient.SqlBulkCopy> 類別，在 SQL Server 的執行個體中單一大量複製資料，以及如何使用 Transact-SQL 陳述式和 <xref:Microsoft.Data.SqlClient.SqlCommand> 類別來執行大量複製作業。  
  
[多項大量複製作業](multiple-bulk-copy-operations.md)  
描述如何使用 <xref:Microsoft.Data.SqlClient.SqlBulkCopy> 類別，在 SQL Server 的執行個體中執行資料的多個大量複製作業。  
  
[交易和大量複製作業](transaction-bulk-copy-operations.md)  
描述如何在交易內執行大量複製作業，包括如何認可或復原交易。  
  
## <a name="next-steps"></a>後續步驟
- [SQL Server and ADO.NET](index.md) (SQL Server 和 ADO.NET)

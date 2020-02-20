---
title: ADO.NET 中的 SQL Server 資料作業
description: 說明如何使用 SQL Server 中的資料。 包含大量複製作業、MARS、非同步作業和資料表值參數的相關章節。
ms.date: 08/15/2019
ms.assetid: b864ebc9-ed8e-4059-85fd-36d9198f5521
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 3f435e44ef6fb7fb7ff777e2b5361482fcde9a98
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "75251110"
---
# <a name="sql-server-data-operations-in-adonet"></a>ADO.NET 中的 SQL Server 資料作業

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下載 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

此節描述 Microsoft SqlClient Data Provider for SQL Server (<xref:Microsoft.Data.SqlClient>) 特有的 SQL Server 特性和功能。  
  
## <a name="in-this-section"></a>本節內容  
[SQL Server 中的大量複製作業](bulk-copy-operations-sql-server.md)  
說明 .NET Data Provider for SQL Server 的大量複製功能。  
  
[Multiple Active Result Set (MARS)](multiple-active-result-sets-mars.md)  
描述從個別命令啟動 <xref:Microsoft.Data.SqlClient.SqlDataReader> 的每個執行個體時，如何在連線上開啟一個以上的 <xref:Microsoft.Data.SqlClient.SqlDataReader>。  
  
[非同步作業](asynchronous-operations.md)  
說明如何使用在 .NET Framework 所用非同步模型之後建立模型的 API，來執行非同步資料庫作業。  
  
[資料表值參數](table-valued-parameters.md)  
描述如何使用在 SQL Server 2008 中引進的資料表值參數。  
  
## <a name="next-steps"></a>後續步驟
- [SQL Server and ADO.NET](index.md) (SQL Server 和 ADO.NET)

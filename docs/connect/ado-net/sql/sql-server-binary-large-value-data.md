---
title: SQL Server 二進位和大型數值資料
description: 說明如何在 SQL Server 中使用大型數值資料。
ms.date: 08/15/2019
ms.assetid: e00827b3-7511-4b2d-91d7-851ca86cc6b5
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: e60f8ce6bc8e7ef05a2de942d8bbc2885095d493
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "75251118"
---
# <a name="sql-server-binary-and-large-value-data"></a>SQL Server 二進位和大型數值資料

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下載 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

SQL Server 提供 `max` 指定名稱，可擴充 `varchar`、`nvarchar` 和 `varbinary` 資料類型的儲存容量。 `varchar(max)`、`nvarchar(max)` 和 `varbinary(max)` 統稱為「大數值資料類型」  。 您可以使用大數值資料類型來儲存最多可達 2^31-1 位元組的資料。  
  
SQL Server 2008 引進了 FILESTREAM 屬性，其不是資料類型，而是可定義於資料行上的屬性，能夠將大數值資料儲存於檔案系統，而不是資料庫中。  
  
## <a name="in-this-section"></a>本節內容  
[修改 ADO.NET 中的大數值 (max) 資料](modify-large-value-max-data.md)  
描述如何使用大數值資料類型。  
  
[FILESTREAM 資料](filestream-data.md)  
描述如何搭配 FILESTREAM 屬性來使用 SQL Server 2008 中所儲存的大數值資料。  
  
## <a name="next-steps"></a>後續步驟
- [SQL Server 資料類型和 ADO.NET](sql-server-data-types.md)
- [ADO.NET 中的 SQL Server 資料作業](sql-server-data-operations.md)

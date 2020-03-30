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
ms.openlocfilehash: 4ed8ccbadb27008fb15d9d117d55b5a4d332a8f6
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "78896623"
---
# <a name="sql-server-binary-and-large-value-data"></a>SQL Server 二進位和大型數值資料

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

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

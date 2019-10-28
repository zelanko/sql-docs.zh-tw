---
title: SQL Server 二進位和大型數值資料
description: 說明如何在 SQL Server 中使用大型數值資料。
ms.date: 08/15/2019
ms.assetid: e00827b3-7511-4b2d-91d7-851ca86cc6b5
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 0a38d90a810f9ca3ee376562eaabf6e713267b27
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452056"
---
# <a name="sql-server-binary-and-large-value-data"></a>SQL Server 二進位和大型數值資料

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下載 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

SQL Server 提供 `max` 規範，它會展開 `varchar`、`nvarchar` 和 `varbinary` 資料類型的儲存容量。 `varchar(max)`、`nvarchar(max)` 和 `varbinary(max)` 統稱為「大數值資料類型」  。 您可以使用大數值資料類型來儲存最多可達 2^31-1 位元組的資料。  
  
SQL Server 2008 引進了 FILESTREAM 屬性，這不是資料類型，而是可定義于資料行的屬性，允許將大數值資料儲存在檔案系統，而不是資料庫中。  
  
## <a name="in-this-section"></a>本節內容  
[修改 ADO.NET 中的大數值 (max) 資料](modify-large-value-max-data.md)  
描述如何使用大數值資料類型。  
  
[FILESTREAM 資料](filestream-data.md)  
描述如何使用以 FILESTREAM 屬性儲存在 SQL Server 2008 中的大數值資料。  
  
## <a name="next-steps"></a>後續步驟
- [SQL Server 資料類型和 ADO.NET](sql-server-data-types.md)
- [ADO.NET 中的 SQL Server 資料作業](sql-server-data-operations.md)

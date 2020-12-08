---
title: 擷取及修改資料
description: 在 .NET Framework 中，Microsoft SqlClient Data Provider for SQL Server 可作為應用程式與資料來源之間的橋樑來讀取及更新資料。
ms.date: 11/13/2020
ms.assetid: 722e7f87-3691-46c6-87e8-7d159722d675
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 8fc6a8ed3cf4fec9b97b81c38fb1667588623ba7
ms.sourcegitcommit: debaff72dbfae91b303f0acd42dd6d99e03135a2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/01/2020
ms.locfileid: "96419732"
---
# <a name="retrieving-and-modifying-data-in-adonet"></a>在 ADO.NET 中擷取及修改資料

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

任何資料庫應用程式都有一個主要功能，那就是連接到資料來源並擷取其內含的資料。 SqlClient 資料提供者可作為應用程式與資料來源之間的橋樑，讓您能夠執行命令，以及使用 **DataReader** 或 **DataAdapter** 來擷取資料。 任何資料庫應用程式都有一個主要功能，那就是更新資料庫中儲存的資料。 在 Microsoft SqlClient Data Provider for SQL Server 中，更新資料牽涉到使用 **DataAdapter** 與 <xref:System.Data.DataSet>，以及 **Command** 物件；而且也可能涉及使用異動。

## <a name="in-this-section"></a>本節內容

[連線到資料來源](connecting-to-data-source.md) 描述如何建立與資料來源的連線，以及如何使用連線事件。

[連接字串](connection-strings.md) 包含描述使用、儲存及擷取連接字串 (包含連接字串關鍵字、安全性資訊) 之各種層面的主題。

[連接共用](connection-pooling.md) 描述適用於 Microsoft SqlClient Data Provider for SQL Server 的連接共用。

## <a name="see-also"></a>請參閱

- [ADO.NET 中的資料類型對應](data-type-mappings-ado-net.md)
- [SQL Server and ADO.NET](./sql/index.md) (SQL Server 和 ADO.NET)

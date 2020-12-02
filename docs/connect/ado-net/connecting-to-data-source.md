---
title: 連線到資料來源
description: 了解用來連線到 ADO.NET 中資料來源的 Connection 物件。 您選擇的 Connection 物件取決於資料來源的類型。
ms.date: 11/13/2020
ms.assetid: 9abc3f92-1be3-4e1a-b360-762dc689650e
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: ab6edc2a7090de85e970445cdb2b86d6ed5cb8f2
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/25/2020
ms.locfileid: "96126428"
---
# <a name="connecting-to-a-data-source-in-adonet"></a>連線到 ADO.NET 中的資料來源

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

在 Microsoft SqlClient 資料提供者中，您可以透過在連接字串中提供必要的驗證資訊，使用 **Connection** 物件連線到特定的資料來源。 您使用的 **Connection** 物件取決於資料來源的類型。

Microsoft SqlClient Data Provider for SQL Server 包括衍生自 <xref:System.Data.Common.DbConnection> 類別的 <xref:Microsoft.Data.SqlClient.SqlConnection> 類型。

## <a name="in-this-section"></a>本節內容  

[建立連線](establishing-connection.md)\
描述如何使用 **Connection** 物件來建立資料來源的連線。

[連線事件](connection-events.md)\
描述如何使用 **InfoMessage** 事件，從資料來源擷取參考訊息。

## <a name="see-also"></a>另請參閱

- [連接字串](connection-strings.md)
- [連接共用](connection-pooling.md)

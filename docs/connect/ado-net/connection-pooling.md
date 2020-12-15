---
title: 連線共用
description: 了解連接共用，ADO.NET 可以使用這種最佳化技術，來將開啟連線到資料來源的成本降至最低。
ms.date: 11/13/2020
ms.assetid: 955c057f-aea8-4ba8-aa6d-e3dfa18ba8d5
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 41b139d2f22a9cb3137879d96224b02eafc24bab
ms.sourcegitcommit: c127c0752e84cccd38a7e23ac74c0362a40f952e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/07/2020
ms.locfileid: "96761496"
---
# <a name="connection-pooling"></a>連線共用

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

連接至資料來源可能會很耗時。 為了將開啟連線的成本降至最低，ADO.NET 使用稱為「連接共用」的最佳化技術，來將重複開啟及關閉連線的成本降至最低。

## <a name="in-this-section"></a>本節內容  

[SQL Server 連接共用 (ADO.NET)](sql-server-connection-pooling.md)  
提供連接共用的概觀並描述連接共用如何在 SQL Server 中運作。

## <a name="see-also"></a>另請參閱

- [在 ADO.NET 中傳送和修改資料](retrieving-modifying-data.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)

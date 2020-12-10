---
title: 使用命令來修改資料
description: 說明如何使用資料提供者來執行預存程序 (Stored Procedure) 或資料定義語言 (DDL) 陳述式。
ms.date: 11/25/2020
ms.assetid: f4160389-b9ff-4b74-b655-437c76dcd586
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 98127e41b5b07c38030ef27214c9c92bf7c4b4be
ms.sourcegitcommit: c127c0752e84cccd38a7e23ac74c0362a40f952e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/07/2020
ms.locfileid: "96761476"
---
# <a name="using-commands-to-modify-data"></a>使用命令來修改資料

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

透過使用 Microsoft SqlClient Data Provider for SQL Server，您可以執行預存程序或資料定義語言 (Data Definition Language) 陳述式 (例如 CREATE TABLE 與 ALTER COLUMN)，以在資料庫或目錄上執行結構描述操作。 這些命令不會像查詢一樣傳回資料列，因此 <xref:Microsoft.Data.SqlClient.SqlCommand> 物件會提供 <xref:Microsoft.Data.SqlClient.SqlCommand.ExecuteNonQuery%2A> 來加以處理。

除了使用 **ExecuteNonQuery** 來修改結構描述之外，您也可以使用這個方法來處理能修改資料但不會傳回資料列的 SQL 陳述式，例如 INSERT、UPDATE 與 DELETE。

雖然 **ExecuteNonQuery** 方法不會傳回資料列，但輸入與輸出參數，以及傳回值都可以透過 **Command** 物件的 **Parameters** 集合來傳遞及傳回。

## <a name="in-this-section"></a>本節內容

[更新資料來源中的資料](update-data-inside-data-source.md)  
說明如何執行修改資料庫資料的命令或預存程序。

[執行目錄作業](perform-catalog-operations.md)  
說明如何執行修改資料庫結構描述的命令。

## <a name="see-also"></a>請參閱

- [在 ADO.NET 中擷取及修改資料](retrieving-modifying-data.md)
- [命令與參數](commands-parameters.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)

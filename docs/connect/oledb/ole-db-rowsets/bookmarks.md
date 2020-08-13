---
title: 資料列書籤 (OLE DB 驅動程式) | Microsoft Docs
description: OLE DB Driver for SQL Server 中的書籤
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- bookmarks [OLE DB]
- OLE DB Driver for SQL Server, bookmarks
- rowsets [OLE DB], bookmarks
- OLE DB rowsets, bookmarks
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 4065ae08fe37b42e47ae464a09d2a9e2a9810bb7
ms.sourcegitcommit: 591bbf4c7e4e2092f8abda6a2ffed263cb61c585
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86942250"
---
# <a name="bookmarks"></a>書籤
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  書籤可讓取用者快速地返回資料列。 取用者可以利用書籤，根據書籤值隨機存取資料列。 書籤資料行在資料列集中為資料行 0。 取用者會將繫結結構的 dwFlag 欄位值設定為 DBCOLUMNSINFO_ISBOOKMARK，表示該資料行會當做書籤使用。 取用者也會將資料列集屬性 DBPROP_BOOKMARKS 設定為 VARIANT_TRUE。 這可讓資料行 0 出現在資料列集中。 然後使用 **IRowsetLocate::GetRowsAt** 方法來擷取資料列，從書籤中指定為位移的資料列開始。  
  
## <a name="see-also"></a>另請參閱  
 [資料列集](../../oledb/ole-db-rowsets/rowsets.md)  
  
  

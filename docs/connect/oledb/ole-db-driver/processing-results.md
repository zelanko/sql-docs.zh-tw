---
title: 處理結果 |Microsoft Docs
description: 處理結果
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, results processing
- OLE DB, processing results
- rowsets [SQL Server], results processing
- results [OLE DB Driver for SQL Server]
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 9d29e75f75332f207c64a7b502e60300e9aae3d5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67994977"
---
# <a name="processing-results"></a>處理結果
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  如果資料列集物件是由命令的執行所產生或是直接從提供者產生資料列集物件而產生，則取用者需要擷取及存取此資料列集中的資料。  
  
 資料列集是可讓 OLE DB 驅動程式 SQL Server 以表格形式公開資料的中央物件。 就概念上來說，資料列集是一組資料列，其中各個資料列都有資料行。 資料列集物件會公開介面，例如 **IRowset** (其中包含一些方法來從資料列集循序擷取資料列)、**IAccessor** (允許一組資料行繫結的定義，以描述表格式資料繫結至取用者程式變數的方式)、**IColumnsInfo** (提供有關資料列集內之資料行的資訊) 及 **IRowsetInfo** (提供有關資料列集的資訊)。  
  
 取用者可以呼叫 **IRowset::GetData** 方法，將資料列集中的資料列擷取到緩衝區。 在呼叫 **GetData** 之前，取用者會使用一組 DBBINDING 結構來描述緩衝區。 每一個繫結都會描述資料列集中的資料行是如何儲存在取用者緩衝區內，並包含以下項目：  
  
-   套用繫結之資料行 (或參數) 的序數。  
  
-   有關繫結內容的資訊 (例如資料值、資料的長度和它的繫結狀態)。  
  
-   有關緩衝區內對每一個部分之位移的資訊。  
  
-   存在於取用者緩衝區內之資料值的長度和類型。  
  
 當取得資料時，提供者會使用每一個繫結中的資訊來判斷要從取用者緩衝區的何處擷取資料以及擷取方式為何。 在取用者緩衝區內設定資料時，提供者會使用每一個繫結中的資訊來判斷要從取用者緩衝區的何處傳回資料以及傳回方式為何。  
  
 當指定了 DBBINDING 結構之後，就會建立存取子 (**IAccessor::CreateAccessor**)。 存取子是繫結的集合，可用來取得或設定取用者緩衝區內的資料。  
  
## <a name="see-also"></a>另請參閱  
 [建立 OLE DB Driver for SQL Server 應用程式](../../oledb/ole-db-driver/creating-a-oledb-driver-for-sql-server-application.md)   
 [OLE DB 的使用說明主題](../../oledb/ole-db-how-to/ole-db-how-to-topics.md)  
  
  

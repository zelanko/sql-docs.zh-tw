---
title: 處理結果 |Microsoft 文件
description: 處理結果
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb-driver-for-sql-server
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, results processing
- OLE DB, processing results
- rowsets [SQL Server], results processing
- results [OLE DB Driver for SQL Server]
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 3e157a115fcc0efd1935a1caa86da18d9afe7c71
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="processing-results"></a>處理結果
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  如果資料列集物件是由命令的執行所產生或是直接從提供者產生資料列集物件而產生，則取用者需要擷取及存取此資料列集中的資料。  
  
 資料列集是中央物件，可啟用 SQL Server，以公開在表格式表單中的資料，OLE DB 驅動程式。 就概念上來說，資料列集是一組資料列，其中各個資料列都有資料行。 資料列集物件會將介面公開這類**IRowset** （包含從資料列集循序提取資料列的方法） **IAccessor** （允許群組的資料行繫結描述表格式資料繫結至取用者程式變數的方式定義）， **IColumnsInfo** （提供有關資料列集中的資料行） 和**IRowsetInfo** （提供資料列集的相關資訊）。  
  
 取用者可以呼叫**irowset:: Getdata**讀入緩衝區中擷取資料列集的資料列的方法。 之前**GetData**是取用者呼叫，描述使用 DBBINDING 結構的一組緩衝區。 每一個繫結都會描述資料列集中的資料行是如何儲存在取用者緩衝區內，並包含以下項目：  
  
-   套用繫結之資料行 (或參數) 的序數。  
  
-   有關繫結內容的資訊 (例如資料值、資料的長度和它的繫結狀態)。  
  
-   有關緩衝區內對每一個部分之位移的資訊。  
  
-   存在於取用者緩衝區內之資料值的長度和類型。  
  
 當取得資料時，提供者會使用每一個繫結中的資訊來判斷要從取用者緩衝區的何處擷取資料以及擷取方式為何。 在取用者緩衝區內設定資料時，提供者會使用每一個繫結中的資訊來判斷要從取用者緩衝區的何處傳回資料以及傳回方式為何。  
  
 指定了 DBBINDING 結構之後，會建立存取子 (**iaccessor:: Createaccessor**)。 存取子是繫結的集合，可用來取得或設定取用者緩衝區內的資料。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 應用程式建立 OLE DB 驅動程式](../../oledb/ole-db-driver/creating-a-oledb-driver-for-sql-server-application.md)   
 [OLE DB 的使用說明主題](../../oledb/ole-db-how-to/ole-db-how-to-topics.md)  
  
  

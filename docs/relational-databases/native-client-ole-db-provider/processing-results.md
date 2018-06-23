---
title: 處理結果 |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db-provider
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, results processing
- OLE DB, processing results
- rowsets [SQL Server], results processing
- results [SQL Server Native Client]
ms.assetid: 20887ac4-f649-4e7f-92e6-f929e2e70952
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 18dddb9c3244a50a81d64b25fa200ca16e634284
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2018
ms.locfileid: "35699949"
---
# <a name="processing-results"></a>處理結果
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  如果資料列集物件是由命令的執行所產生或是直接從提供者產生資料列集物件而產生，則取用者需要擷取及存取此資料列集中的資料。  
  
 資料列集是中央物件，可讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者以表格式格式公開資料。 就概念上來說，資料列集是一組資料列，其中各個資料列都有資料行。 資料列集物件會將介面公開這類**IRowset** （包含從資料列集循序提取資料列的方法） **IAccessor** (允許的資料行繫結描述的群組定義方法的表格式資料繫結至取用者程式變數）， **IColumnsInfo** （提供有關資料列集中的資料行） 和**IRowsetInfo** （提供資料列集的相關資訊）。  
  
 取用者可以呼叫**irowset:: Getdata**讀入緩衝區中擷取資料列集的資料列的方法。 之前**GetData**是取用者呼叫，描述使用 DBBINDING 結構的一組緩衝區。 每一個繫結都會描述資料列集中的資料行是如何儲存在取用者緩衝區內，並包含以下項目：  
  
-   套用繫結之資料行 (或參數) 的序數。  
  
-   有關繫結內容的資訊 (例如資料值、資料的長度和它的繫結狀態)。  
  
-   有關緩衝區內對每一個部分之位移的資訊。  
  
-   存在於取用者緩衝區內之資料值的長度和類型。  
  
 當取得資料時，提供者會使用每一個繫結中的資訊來判斷要從取用者緩衝區的何處擷取資料以及擷取方式為何。 在取用者緩衝區內設定資料時，提供者會使用每一個繫結中的資訊來判斷要從取用者緩衝區的何處傳回資料以及傳回方式為何。  
  
 指定了 DBBINDING 結構之後，會建立存取子 (**iaccessor:: Createaccessor**)。 存取子是繫結的集合，可用來取得或設定取用者緩衝區內的資料。  
  
## <a name="see-also"></a>另請參閱  
 [建立 SQL Server Native Client OLE DB 提供者應用程式](../../relational-databases/native-client-ole-db-provider/creating-a-sql-server-native-client-ole-db-provider-application.md)   
 [OLE DB 的使用說明主題](../../relational-databases/native-client-ole-db-how-to/ole-db-how-to-topics.md)  
  
  

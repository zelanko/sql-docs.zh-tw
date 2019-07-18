---
title: 處理結果 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
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
ms.openlocfilehash: 9fdc66899f7d863cbfb3ae04ad0796614717a734
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63209668"
---
# <a name="processing-results"></a>處理結果
  如果資料列集物件是由命令的執行所產生或是直接從提供者產生資料列集物件而產生，則取用者需要擷取及存取此資料列集中的資料。  
  
 資料列集是中央物件，可讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者以表格式格式公開資料。 就概念上來說，資料列集是一組資料列，其中各個資料列都有資料行。 資料列集物件會公開介面，例如 **IRowset** (其中包含一些方法來從資料列集循序擷取資料列)、**IAccessor** (允許一組資料行繫結的定義，以描述表格式資料繫結至取用者程式變數的方式)、**IColumnsInfo** (提供有關資料列集內之資料行的資訊) 及 **IRowsetInfo** (提供有關資料列集的資訊)。  
  
 取用者可以呼叫 **IRowset::GetData** 方法，將資料列集中的資料列擷取到緩衝區。 在呼叫 **GetData** 之前，取用者會使用一組 DBBINDING 結構來描述緩衝區。 每一個繫結都會描述資料列集中的資料行是如何儲存在取用者緩衝區內，並包含以下項目：  
  
-   套用繫結之資料行 (或參數) 的序數。  
  
-   有關繫結內容的資訊 (例如資料值、資料的長度和它的繫結狀態)。  
  
-   有關緩衝區內對每一個部分之位移的資訊。  
  
-   存在於取用者緩衝區內之資料值的長度和類型。  
  
 當取得資料時，提供者會使用每一個繫結中的資訊來判斷要從取用者緩衝區的何處擷取資料以及擷取方式為何。 在取用者緩衝區內設定資料時，提供者會使用每一個繫結中的資訊來判斷要從取用者緩衝區的何處傳回資料以及傳回方式為何。  
  
 當指定了 DBBINDING 結構之後，就會建立存取子 (**IAccessor::CreateAccessor**)。 存取子是繫結的集合，可用來取得或設定取用者緩衝區內的資料。  
  
## <a name="see-also"></a>另請參閱  
 [建立 SQL Server Native Client OLE DB 提供者應用程式](creating-a-sql-server-native-client-ole-db-provider-application.md)   
 [OLE DB 的使用說明主題](../native-client-ole-db-how-to/ole-db-how-to-topics.md)  
  
  

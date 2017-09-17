---
title: "延遲欄位 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- descriptors [ODBC], deferred fields
- deferred fields [ODBC]
ms.assetid: 5abeb9cc-4070-4f43-a80d-ad6a2004e5f3
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 38967637f505191a5ff353c13b4ebfbbe08e615a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="deferred-fields"></a>延後的欄位
值*延遲欄位*時設定，但是驅動程式會將儲存延後的效果之變數的位址不會使用。 應用程式參數描述元，驅動程式會使用變數的內容時呼叫的**SQLExecDirect**或**SQLExecute**。 應用程式的資料列描述項，為驅動程式會使用變數的內容，在擷取的時間。  
  
 延後的欄位如下：  
  
-   描述項記錄的 SQL_DESC_DATA_PTR 和 SQL_DESC_INDICATOR_PTR 欄位。  
  
-   應用程式的描述項記錄 SQL_DESC_OCTET_LENGTH_PTR 欄位。  
  
-   如果是多重資料列提取時，SQL_DESC_ARRAY_STATUS_PTR 和 SQL_DESC_ROWS_PROCESSED_PTR 欄位的描述項標頭。  
  
 當配置描述元時，延後的每個描述項記錄欄位一開始會有 null 值。 Null 值的意義如下：  
  
-   如果 SQL_DESC_ARRAY_STATUS_PTR 有 null 值，多重資料列的 fetch 就無法傳回此元件的每個資料列的診斷資訊。  
  
-   如果 SQL_DESC_DATA_PTR 有 null 值，記錄就會是未繫結。  
  
-   如果 ARD 的 SQL_DESC_OCTET_LENGTH_PTR 欄位的 null 值，此驅動程式不會傳回該資料行的長度資訊。  
  
-   如果 APD SQL_DESC_OCTET_LENGTH_PTR 欄位具有 null 值，而且參數為字元字串，驅動程式會假設字串是以 null 結束。 輸出的動態參數，此欄位中的 null 值會防止驅動程式傳回長度資訊。 （如果 SQL_DESC_TYPE 欄位並不表示字元字串參數，SQL_DESC_OCTET_LENGTH_PTR 欄位會忽略。）  
  
 應用程式不能解除配置或捨棄它關聯欄位的時間與驅動程式讀取或寫入它們的時間之間的延遲欄位使用的變數。

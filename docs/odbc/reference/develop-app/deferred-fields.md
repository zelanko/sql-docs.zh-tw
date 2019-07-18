---
title: 延後欄位 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], deferred fields
- deferred fields [ODBC]
ms.assetid: 5abeb9cc-4070-4f43-a80d-ad6a2004e5f3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c2c229d31941d5cef0da253545cecd7d1496ee4a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68076818"
---
# <a name="deferred-fields"></a>延遲的欄位
值*延後欄位*不會設定它們，但驅動程式會將儲存的延後的效果之變數的位址時使用。 應用程式參數描述項中，驅動程式會使用變數的內容呼叫當時**SQLExecDirect**或是**SQLExecute**。 應用程式的資料列描述項中，驅動程式會使用變數的內容在提取的階段。  
  
 延後的欄位如下：  
  
-   描述項記錄的 SQL_DESC_DATA_PTR 並 SQL_DESC_INDICATOR_PTR 欄位。  
  
-   將應用程式描述項記錄 SQL_DESC_OCTET_LENGTH_PTR 欄位。  
  
-   如果是多重資料列提取時，SQL_DESC_ARRAY_STATUS_PTR 和 SQL_DESC_ROWS_PROCESSED_PTR 欄位的描述項標頭。  
  
 當配置描述元時，延遲的欄位，每個描述項記錄的一開始會有 null 值。 Null 值的意義如下所示：  
  
-   如果 SQL_DESC_ARRAY_STATUS_PTR 具有 null 值時，多重資料列的 fetch 無法傳回這個元件的每個資料列的診斷資訊。  
  
-   如果 SQL_DESC_DATA_PTR 具有 null 值時，記錄就會是未繫結。  
  
-   如果 ARD 的 SQL_DESC_OCTET_LENGTH_PTR 欄位具有 null 值時，驅動程式不會傳回該資料行長度資訊。  
  
-   APD 中的 SQL_DESC_OCTET_LENGTH_PTR 欄位具有 null 值，而且參數是字元字串，如果驅動程式會假設字串是 null 結束。 輸出動態參數，此欄位中的 null 值會防止驅動程式傳回長度資訊。 （如果 SQL_DESC_TYPE 欄位不是表示的字元字串參數，SQL_DESC_OCTET_LENGTH_PTR 欄位會忽略。）  
  
 應用程式不解除配置或捨棄用於延後的欄位，它將它們與欄位關聯的時間與驅動程式會讀取或寫入的時間之間的變數。

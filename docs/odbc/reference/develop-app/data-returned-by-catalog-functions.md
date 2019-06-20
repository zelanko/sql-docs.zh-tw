---
title: 目錄函式所傳回的資料 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], result sets
- functions [ODBC], catalog functions
ms.assetid: 399e1a64-8766-4c44-81ff-445399b7a1de
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 10e3726d26e03da2f9f731babc105244dbf1ff05
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63267733"
---
# <a name="data-returned-by-catalog-functions"></a>目錄函式所傳回的資料
每個目錄函式會傳回資料當作結果集。 此結果集是與其他類型的結果集。 它通常就會產生依預先定義參數化**選取**是硬式編碼在驅動程式，或是儲存在資料來源中的程序中的陳述式。 如需如何擷取資料，從結果集資訊，請參閱[結果集建立？](../../../odbc/reference/develop-app/was-a-result-set-created.md)。  
  
 結果集中的每個目錄函式是該函式的參考項目中所述。 除了列出的資料行，結果集可以包含在最後一個預先定義的資料行之後的驅動程式特有的資料行。 驅動程式文件將描述這些資料行 （如果有的話）。  
  
 應用程式應繫結的驅動程式特有的資料行，相對於結果集的結尾。 也就是它們應該計算驅動程式專屬的資料行的數目，做為使用擷取的最後一個資料行數**SQLNumResultCols** -較不必要的資料行之後發生的資料行數目。 ODBC 的版本或驅動程式，這樣不必變更應用程式，新的資料行新增至結果時可節省設定在未來。 此配置中運作，驅動程式必須新增新的驅動程式特有的資料行，舊的驅動程式專用資料行之前，讓資料行號碼並未變更相對於結果集的結尾。  
  
 結果集中傳回的識別項不加上引號，即使它們包含特殊字元。 例如，假設識別項引號字元 (這是由特定驅動程式，以及透過傳回**SQLGetInfo**) 是雙引號 （"），而且 Accounts Payable 資料表包含客戶名稱的資料行。 在所傳回的資料列**SQLColumns**本專欄中，名稱資料行的值是 Accounts Payable，不"Accounts Payable"，和 COLUMN_NAME 資料行的值是客戶名稱，沒有 「 客戶名稱 」。 若要擷取的 Accounts Payable 資料表中的客戶名稱，應用程式會引用這些名稱如下：  
  
```  
SELECT "Customer Name" FROM "Accounts Payable"  
```  
  
 如需詳細資訊，請參閱 <<c0> [ 加上引號的識別項](../../../odbc/reference/develop-app/quoted-identifiers.md)。  
  
 目錄函式根據在其中建立根據使用者名稱和密碼，連線，並傳回使用者有權限的資料類似 SQL 的授權模型。 個別檔案的密碼保護它不符合此模型，是驅動程式定義。  
  
 目錄函式所傳回的結果集可以幾乎不會更新，以及應用程式不應該預期能夠藉由變更這些結果集內的資料變更資料庫的結構。

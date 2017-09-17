---
title: "目錄函數所傳回的資料 |Microsoft 文件"
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
- catalog functions [ODBC], result sets
- functions [ODBC], catalog functions
ms.assetid: 399e1a64-8766-4c44-81ff-445399b7a1de
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 39d795314d2333c5d33cb55057b68e652082ae89
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="data-returned-by-catalog-functions"></a>目錄函數所傳回的資料
每個類別目錄函數會傳回資料當作結果集。 此結果集並無不同的任何其他結果集。 通常是由預先定義參數化**選取**是硬式編碼驅動程式中或預存程序中的資料來源的陳述式。 如需如何從結果集擷取資料資訊，請參閱[已設定建立結果？](../../../odbc/reference/develop-app/was-a-result-set-created.md)。  
  
 結果集中的每個類別目錄函式是該函式的參考項目中所述。 除了列出的資料行，結果集可以包含驅動程式特有的資料行，最後一個預先定義的資料行之後。 這些資料行 （如果有的話） 所述的驅動程式文件。  
  
 應用程式應繫結驅動程式特有的資料行相對於結果集的結尾。 也就是說，它們應該計算驅動程式專用資料行數目的最後一個資料行數目 — 使用擷取**SQLNumResultCols** — 較少的必要資料行之後發生的資料行數目。 ODBC 的版本，或者驅動程式，這需要變更應用程式，加入新的資料行設為該結果時可節省設定在未來。 若要使用此配置，驅動程式必須新增新驅動程式特有的資料行，舊的驅動程式專用資料行之前，讓資料行編號不會變更相對於結果集的結尾。  
  
 結果集中傳回的識別項不加上引號，即使它們包含特殊字元。 例如，假設識別項引號字元 (這是驅動程式專屬，傳回透過**SQLGetInfo**) 是雙引號 （"） 和 Accounts Payable 資料表包含客戶名稱的資料行。 所傳回的資料列中**SQLColumns**此資料行，TABLE_NAME 資料行的值為 Accounts Payable，不"Accounts Payable"，和 COLUMN_NAME 資料行的值是客戶名稱，沒有 「 客戶名稱 」。 若要擷取 Accounts Payable 資料表中客戶的名稱，應用程式會加上引號這些名稱：  
  
```  
SELECT "Customer Name" FROM "Accounts Payable"  
```  
  
 如需詳細資訊，請參閱[引號識別項](../../../odbc/reference/develop-app/quoted-identifiers.md)。  
  
 目錄函數會根據類似 SQL 的授權模型中建立連線時根據使用者名稱和密碼，並傳回使用者有權限的資料。 個別檔案的密碼保護它不符合此模型，為驅動程式定義。  
  
 目錄函數所傳回的結果集可以幾乎永遠不會更新，以及應用程式不應預期要能夠藉由變更這些結果集內的資料變更資料庫的結構。

---
title: "字元資料和 C 字串 |Microsoft 文件"
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
- data buffers [ODBC], length
- data buffers [ODBC], character data
- buffers [ODBC], C strings
- buffers [ODBC], character data
- character data and buffers [ODBC]
- length of data buffers [ODBC]
- data buffers [ODBC], C strings
- buffers [ODBC], length
- C strings and buffers [ODBC]
ms.assetid: 3a141cb4-229d-4027-9349-615cb2995e36
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c786c1ce1ea3457da20d4f50c54ea7b797c70c1b
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="character-data-and-c-strings"></a>字元資料，而且 C 字串
參考 （例如資料行名稱、 動態參數和字串屬性值） 的可變長度的字元資料的輸入的參數都有相關聯的長度參數。 如果應用程式終止的 null 字元，跟一般的 C 字串，它會提供做為引數是以位元組為單位 （不包括 null 結束字元） 字串的長度或 SQL_NTS （Null-Terminated 字串）。 非負數長度的引數指定相關聯的字串的實際長度。 長度引數可能是 0，表示指定零長度字串，也就是不同的 NULL 值。 負值 SQL_NTS 會指示驅動程式尋找 null 結束字元，判斷字串的長度。  
  
 字元資料從驅動程式傳回給應用程式時，驅動程式必須一律以 null 結束它。 這可讓應用程式是否為字串或字元陣列來處理資料的選擇。 如果應用程式緩衝區不夠大，無法傳回的所有字元資料，驅動程式截斷為以 null 結束的字元所需的位元組數目小於緩衝區的位元組長度會截斷的資料，以 null 終止，將其儲存在緩衝區。 因此，應用程式必須一律為用來擷取字元資料的緩衝區中的 null 終止字元配置額外的空間。 例如，擷取 50 個字元的資料需 51 位元組緩衝區。  
  
 應用程式和驅動程式傳送或擷取長時間使用組件中的字元資料時所必須採取特別注意**SQLPutData**或**SQLGetData**。 如果將資料傳送為一系列的 null 結尾字串，這些字串的 null 終止字元必須移除之前可以接收資料。  
  
 字元資料，而且 C 字串，有混淆的 ODBC 程式設計人員的數字。 這是定義 ODBC 函數時，使用 C 語言的成品。 如果 ODBC 驅動程式或應用程式使用另一種語言，記住 ODBC 的語言無關，混淆不太可能會發生。  
  
 C 字串用來保存字元資料，當 null 結束字元不被視為資料的一部分，並不會計入為它的位元組長度的一部分。 例如，可以當做 C 字串"ABC\0 」 或 {'A'、 'B'、 'C'} 的字元陣列保留字元資料"ABC"。 資料的位元組長度為 3，無論它當成字串或字元陣列。  
  
 雖然應用程式和驅動程式通常使用 C 字串 （以 null 結束的字元陣列） 來保存字元資料，但沒有要執行這項操作的需求。 在 C 中，字元資料可以也被視為 （不含 null 終止） 的字元陣列和其個別傳入之長度/指標緩衝區的位元組長度。  
  
 由於非 – null 終端陣列中可以保存字元資料，而且其位元組長度分別傳遞，便可在字元資料中內嵌的 null 字元。 不過，在此情況下 ODBC 函數的行為是未定義，而且很是否驅動程式會處理這正確特定驅動程式。 因此，可互通的應用程式應該永遠會處理可包含內嵌的 null 字元做為二進位資料的字元資料。

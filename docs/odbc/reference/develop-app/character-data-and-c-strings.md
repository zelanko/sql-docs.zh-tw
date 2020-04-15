---
title: 字元資料與 C 字串 :微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7bb25022d4e0c0559f2a8f77b89a4ba26aeba33a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307488"
---
# <a name="character-data-and-c-strings"></a>字元資料和 C 字串
引用可變長度字元資料的輸入參數(如列名、動態參數和字串屬性值)具有關聯的長度參數。 如果應用程式終止帶有 null 字元的字串(如 C 中的典型形式),它將提供字串的長度(不包括空終止符)或SQL_NTS(空端字串)。 非負長度參數指定關聯字串的實際長度。 長度參數可以是 0 來指定零長度字串,該字串與 NULL 值不同。 負值SQL_NTS通過定位空終止字元指示驅動程序確定字串的長度。  
  
 當字元數據從驅動程式返回到應用程式時,驅動程式必須始終為 null 終止。 這使應用程式可以選擇是將數據作為字串還是字元陣列處理。 如果應用程式緩衝區不夠大,無法返回所有字元數據,驅動程式將其截斷到緩衝區的位元組長度,減去 null 終止字元所需的位元數,null 終止截斷的資料,並將其存儲在緩衝區中。 因此,應用程式必須始終為用於檢索字元數據的緩衝區中的空終止字元分配額外的空間。 例如,需要 51 位元組緩衝區來檢索 50 個字元的數據。  
  
 在使用**SQLPutData**或**SQLGetData**以部件發送或檢索長字元數據時,應用程式和驅動程式必須特別注意。 如果資料作為一系列 null 終止字串傳遞,則必須剝離這些字串上的 null 終止字元,然後才能重新組合數據。  
  
 許多 ODBC 程式師混淆了字元數據和 C 字串。 發生這種情況是在定義 ODBC 函數時使用 C 語言的一個工件。 如果 ODBC 驅動程式或應用程式使用另一種語言 ( 請記住 ODBC 與語言無關 ) - 這種混淆不太可能發生。  
  
 當 C 字串用於保存字元數據時,空終止字元不被視為數據的一部分,也不將其計為其位元長度的一部分。 例如,字元數據"ABC"可以作為 C 字串"ABC_0"或字元陣列 ['A'、"B"、"C"*進行維護。 數據的位元組長度為 3,無論它被視為字串還是字元陣列。  
  
 儘管應用程式和驅動程式通常使用 C 字串(空終止字元陣列)來保存字元數據,但不需要執行此操作。 在 C 中,字元數據也可以被視為字元陣列(不作空終止),其位元組長度在長度 / 指示器緩衝區中單獨傳遞。  
  
 由於字元數據可以位於非 null 端接陣列中,並且其位元組長度單獨傳遞,因此可以在字元資料中嵌入空字元。 但是,在這種情況下,ODBC 函數的行為是未定義的,並且驅動程式是否正確處理此操作是特定於驅動程式的。 因此,可互操作的應用程式應始終處理可以包含嵌入的空字元作為二進位資料的字元資料。

---
title: 字元資料和 C 字串 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307488"
---
# <a name="character-data-and-c-strings"></a>字元資料和 C 字串
參考可變長度字元資料的輸入參數（例如資料行名稱、動態參數和字串屬性值）具有相關聯的長度參數。 如果應用程式以 null 字元結束字串（如同 C 中的一般），它會以位元組為單位（不包括 null 結束字元）或 SQL_NTS （以 Null 結束的字串）的形式提供引數。 非負值長度引數會指定相關字串的實際長度。 Length 引數可以是0，以指定長度為零的字串，這與 Null 值不同。 負值 SQL_NTS 會藉由尋找 null 終止字元，指示驅動程式判斷字串的長度。  
  
 從驅動程式將字元資料傳回至應用程式時，驅動程式必須一律以 null 結束。 如此一來，應用程式就可以選擇是否要以字串或字元陣列的形式來處理資料。 如果應用程式緩衝區的大小不足以傳回所有的字元資料，驅動程式會將它截斷成緩衝區的位元組長度，而不是 null 終止字元所需的位元組數，以 null 終止截斷的資料，並將其儲存在緩衝區中。 因此，應用程式必須一律在用來捕獲字元資料的緩衝區中，為 null 終止字元配置額外的空間。 例如，需要51位元組的緩衝區，才能取出50個字元的資料。  
  
 在使用**SQLPutData**或**SQLGetData**的部分傳送或抓取長字元資料時，應用程式和驅動程式都必須特別小心。 如果資料是以一系列以 null 結束的字串來傳遞，則必須先移除這些字串上的 null 終止字元，才能將資料重新組合。  
  
 許多 ODBC 程式設計人員都有混淆的字元資料和 C 字串。 這是在定義 ODBC 函數時使用 C 語言的構件。 如果 ODBC 驅動程式或應用程式使用另一種語言，請記住 ODBC 與語言無關-這種混淆較不可能發生。  
  
 當 C 字串用來保存字元資料時，不會將 null 終止字元視為資料的一部分，而且不會計入其位元組長度的一部分。 例如，字元資料 "ABC" 可以保留為 C 字串 "ABC\0"，或字元陣列 {' A '，' B '，' C '}。 資料的位元組長度是3，不論是視為字串或字元陣列。  
  
 雖然應用程式和驅動程式通常會使用 C 字串（以 null 結束的字元陣列）來保存字元資料，但不需要這麼做。 在 C 中，字元資料也可以視為字元陣列（不含 null 終止），而且其位元組長度會分別在長度/指標緩衝區中傳遞。  
  
 因為字元資料可以保存在非 null 結束的陣列中，而且其位元組長度是分開傳遞，所以可以在字元資料中內嵌 null 字元。 不過，在此情況下，ODBC 函式的行為是未定義的，而且它是驅動程式特有的，不論驅動程式是否正確地處理此功能。 因此，互通的應用程式應該一律處理可以包含內嵌 null 字元做為二進位資料的字元資料。

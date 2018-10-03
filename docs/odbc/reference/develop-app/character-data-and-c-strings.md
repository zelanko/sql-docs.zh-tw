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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: df2afd988e46692f816c22e69a31b33833129ff1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47809386"
---
# <a name="character-data-and-c-strings"></a>字元資料和 C 字串
參考 （例如資料行名稱、 動態參數和字串屬性值） 的可變長度的字元資料的輸入的參數都有相關聯的長度參數。 如果應用程式會終止具有 null 字元，跟一般的 C 字串，它會提供做為引數是以位元組為單位 （不包括 null 結束字元） 字串的長度或 SQL_NTS （Null-Terminated 字串）。 非負數長度的引數會指定關聯的字串的實際長度。 長度引數可以是 0，表示指定零長度字串，也就是不同的 NULL 值。 負值 sql_nts; 會指示驅動程式，以找出之 null 結束字元，藉以判斷字串的長度。  
  
 當字元資料的驅動程式傳回給應用程式時，驅動程式必須一律以 null 結束它。 這可讓應用程式選擇是否要處理的資料為字串或字元陣列。 如果應用程式緩衝區不夠大，無法傳回所有字元資料，驅動程式截斷為以 null 終止字元所需的位元組數目小於緩衝區的位元組長度會截斷的資料，以 null 終止，將其儲存在緩衝區。 因此，應用程式永遠必須配置額外的空間用來擷取字元資料的緩衝區中的 null 終止字元。 比方說，擷取資料的 50 個字元需 51 位元組緩衝區。  
  
 應用程式和驅動程式傳送或擷取長時間使用組件中的字元資料時所必須採取特別注意**SQLPutData**或是**SQLGetData**。 如果資料被當做一系列的 null 終止的字串，可以重組資料之前，必須加以移除對這些字串的 null 終止字元。  
  
 ODBC 程式設計人員一些有在字元資料，而且 C 字串混淆。 已發生這是定義 ODBC 函數時，使用 C 語言的成品。 如果 ODBC 驅動程式或應用程式使用另一種語言，請記住，ODBC 語言無關，混淆不太可能發生。  
  
 C 字串用來保存字元資料，當 null 結束字元不被視為資料的一部分，就不會計算其位元組長度的一部分。 比方說，可以保留字元資料"ABC"的 C 字串"ABC\0 」 為 {'A'、 'B'、 'C'} 的字元陣列。 資料的位元組長度為 3，，會被視為字串或字元陣列。  
  
 雖然應用程式和驅動程式通常使用 C 字串 （以 null 結尾的字元陣列） 來保存字元資料，但沒有要執行這項操作的需求。 在 C 中，字元的資料也可以視為 （不含 null 終止） 的字元陣列以及其個別傳入之長度/指標緩衝區的位元組長度。  
  
 因為非 – null 終端陣列中可以保存字元資料，而且它的位元組長度個別傳遞，就可以將內嵌 null 字元的字元資料中。 不過，在此情況下 ODBC 函數的行為是未定義，而且驅動程式專屬是否驅動程式會處理此正確。 因此，互通的應用程式應該一律處理可以包含內嵌的 null 字元做為二進位資料的字元資料。

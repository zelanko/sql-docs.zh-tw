---
description: 字元資料和 C 字串
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
ms.openlocfilehash: e412976cb297af9a9e38bbc6991647eeab48483b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465920"
---
# <a name="character-data-and-c-strings"></a>字元資料和 C 字串
參考可變長度字元資料 (的輸入參數，例如資料行名稱、動態參數和字串屬性值) 有相關聯的長度參數。 如果應用程式以 null 字元結束字串（如同 C 中的一般），則會以字串的長度（以位元組為單位）提供引數， (不包括 null 結束字元) 或 SQL_NTS (以 Null 結尾的字串) 。 非負長度的引數會指定相關聯字串的實際長度。 長度引數可以是0，以指定零長度的字串，此字串與 Null 值相異。 負數值 SQL_NTS 會藉由尋找 null 終止字元來指示驅動程式判斷字串的長度。  
  
 當字元資料從驅動程式傳回給應用程式時，驅動程式必須一律以 null 結束。 如此一來，應用程式就可以選擇是否要將資料當作字串或字元陣列來處理。 如果應用程式緩衝區不夠大，無法傳回所有的字元資料，驅動程式會將它截斷為緩衝區的位元組長度，而不是 null 終止字元所需的位元組數目，null-結束截斷的資料，並將其儲存在緩衝區中。 因此，應用程式一律必須在用來取出字元資料的緩衝區中，為 null 終止字元配置額外的空間。 例如，需要51位元組緩衝區才能取出50字元的資料。  
  
 在使用 **SQLPutData** 或 **SQLGetData**的元件中傳送或抓取長字元資料時，應用程式和驅動程式必須採取特別注意。 如果資料是以一系列以 null 結尾的字串來傳遞，則必須先移除這些字串的 null 終止字元，才能將資料重新組合。  
  
 有許多 ODBC 程式設計人員都有混淆的字元資料和 C 字串。 發生這種情況時，是在定義 ODBC 函數時使用 C 語言的構件。 如果 ODBC 驅動程式或應用程式使用另一種語言-請記住 ODBC 與語言無關，這種混淆比較不可能發生。  
  
 當使用 C 字串來保存字元資料時，不會將 null 終止字元視為資料的一部分，也不會計算為其位元組長度的一部分。 例如，字元資料 "ABC" 可以保留為 C 字串 "ABC\0" 或字元陣列 {' A '、' B '、' C '}。 資料的位元組長度是3，不論它是否被視為字串或字元陣列。  
  
 雖然應用程式和驅動程式通常會使用 C 字串 (以 null 結束的字元陣列) 來保存字元資料，但不需要這麼做。 在 C 中，字元資料也可以視為字元陣列 (不含 null 終止) ，而且其位元組長度會在長度/指標緩衝區中分開傳遞。  
  
 由於字元資料可以保留在非以 null 結尾的陣列中，而且其位元組長度會分開傳遞，因此可以在字元資料中內嵌 null 字元。 不過，在此情況下，ODBC 函式的行為是未定義的，而且它是驅動程式特定的驅動程式是否正確地處理這項功能。 因此，互通的應用程式應該一律處理可包含內嵌 null 字元做為二進位資料的字元資料。

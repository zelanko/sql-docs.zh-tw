---
title: 轉換規則 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- numeric data type [ODBC], literals
- conversions with numeric literals [ODBC]
- numeric literals [ODBC]
- literals [ODBC], numeric
ms.assetid: 89f846a3-001d-496a-9843-ac9c38dc1762
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9ca64355a80ce8892f0ea0494e165d934d8d7a88
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68057087"
---
# <a name="rules-for-conversions"></a>轉換規則
本節中的規則適用于涉及數值常值的轉換。 基於這些規則的用途，會定義下列詞彙：  
  
-   *存放區指派：* 將資料傳送至資料庫中的資料表資料行時。 這會在呼叫**SQLExecute**、 **SQLExecDirect**和**SQLSetPos**時發生。 在存放區指派期間，「目標」是指資料庫資料行，而「來源」則是指應用程式緩衝區中的資料。  
  
-   抓取*指派：* 將資料庫中的資料抓取至應用程式緩衝區時。 這會在呼叫**SQLFetch**、 **SQLGetData**、 **SQLFetchScroll**和**SQLSetPos**時發生。 在抓取指派期間，「目標」是指應用程式緩衝區，而「來源」則是指資料庫資料行。  
  
-   *CS：* 字元來源中的值。  
  
-   *NT：* 數值目標中的值。  
  
-   *NS：* 數值來源中的值。  
  
-   *CT：* 字元目標中的值。  
  
-   精確數值常值的精確度：它所包含的位數。  
  
-   精確數值常值的小數位數：表示或隱含期間右邊的位數。  
  
-   近似數值常值的有效位數：其尾數的有效位數。  
  
## <a name="character-source-to-numeric-target"></a>數位目標的字元來源  
 以下是從字元來源（CS）轉換成數值目標（NT）的規則：  
  
1.  將 CS 取代為移除 CS 中任何前置或尾端空格所取得的值。 如果 CS 不是有效的*數值常*值，則會傳回 SQLSTATE 22018 （cast 規格的無效字元值）。  
  
2.  以取得的值取代 CS，方法是移除小數點前面的前置零、小數點後面的尾端零，或兩者。  
  
3.  將 CS 轉換成 NT。 如果轉換導致大量的數位遺失，則會傳回 SQLSTATE 22003 （超出範圍的數值）。 如果轉換導致 nonsignificant 數位遺失，則會傳回 SQLSTATE 01S07 （小數截斷）。  
  
## <a name="numeric-source-to-character-target"></a>數值來源到字元目標  
 以下是從數值來源（NS）轉換成字元目標（CT）的規則：  
  
1.  讓 LT 做為 CT 的字元長度。 針對抓取指派，LT 等於緩衝區的長度，以字元為單位減去此字元集的 null 終止字元中的位元組數目。  
  
2.  種  
  
    -   如果 NS 是精確的數數值型別，請讓 YP 等於符合*精確數值常*值定義的最短字元字串，這樣一來，YP 的小數位數與 ns 的大小相同，而 YP 的解讀值是 ns 的絕對值。  
  
    -   如果 NS 是近似的數數值型別，請讓 YP 成為字元字串，如下所示：  
  
         案例：  
  
         如果 NS 等於0，則 YP 為0。  
  
         讓 YSN 成為符合精確*數值常*值定義的最短字元字串，而其解讀值是 NS 的絕對值。 如果 YSN 的長度小於 NS 資料類型的（*精確度*+ 1），則 let YP 等於 YSN。  
  
         否則，YP 是符合*近似數值常*值定義的最短字元字串，其解讀值為 NS 的絕對值，而其*尾數*是由不是 ' 0 ' 的單一*數位*組成，後面接著*句號*和不*帶正負號的整數*。  
  
3.  案例：  
  
    -   如果 NS 小於0，則讓 Y 成為的結果：  
  
         '-'  &#124;&#124; YP  
  
         其中 ' &#124;&#124; ' 是字串串連運算子。  
  
         否則，讓 Y 等於 YP。  
  
4.  讓去年年初成為 Y 的字元長度。  
  
5.  案例：  
  
    -   如果去年年初等於 LT，則會將 CT 設定為 Y。  
  
    -   如果去年年初小於 LT，則會將 [CT] 設定為右邊的 [Y] 延伸，適當的空間數目。  
  
         否則（去年年初 > LT），請將 Y 的第一個 LT 字元複製到 CT。  
  
         案例：  
  
         如果這是存放區指派，則傳回錯誤 SQLSTATE 22001 （字串資料，以滑鼠右鍵截斷）。  
  
         如果這是抓取指派，則會傳回警告 SQLSTATE 01004 （字串資料，以滑鼠右鍵截斷）。 當複製導致小數位數遺失（除了尾端零以外）時，它是由驅動程式定義的，不論是否發生下列其中一種情況：  
  
         （1）驅動程式會將 Y 中的字串截斷為適當的小數值（也可以為零），並將結果寫入到 CT。  
  
         （2）驅動程式會將 Y 的字串四捨五入為適當的小數位數值（也可以為零），並將結果寫入到 CT。  
  
         （3）驅動程式既不會截斷也不會四捨五入，只會將 Y 的第一個 LT 字元複製到 CT。

---
description: 轉換規則
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8e3d9a931a960ce1bd404b6616b4a6e4f0d37c4a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424950"
---
# <a name="rules-for-conversions"></a>轉換規則
本節中的規則適用于涉及數值常值的轉換。 基於這些規則的目的，會定義下列詞彙：  
  
-   *存放區指派：* 將資料傳送至資料庫中的資料表資料行時。 這會在呼叫 **SQLExecute**、 **SQLExecDirect**和 **SQLSetPos**期間發生。 在存放區指派期間，「目標」指的是資料庫資料行，而「來源」是指應用程式緩衝區中的資料。  
  
-   抓取*指派：* 從資料庫將資料取出至應用程式緩衝區時。 這會在呼叫 **SQLFetch**、 **SQLGetData**、 **SQLFetchScroll**和 **SQLSetPos**期間發生。 在抓取指派期間，「目標」指的是應用程式緩衝區，而「來源」則是指資料庫資料行。  
  
-   *CS：* 字元來源中的值。  
  
-   *NT：* 數值目標中的值。  
  
-   *NS：* 數值來源中的值。  
  
-   *CT：* 字元目標中的值。  
  
-   精確數值常值的精確度：它所包含的位數。  
  
-   精確數值常值的小數位數：表示或隱含句點右邊的位數。  
  
-   近似數值常值的有效位數：其尾數的精確度。  
  
## <a name="character-source-to-numeric-target"></a>目標為數值目標的字元來源  
 以下是從字元來源 (CS) 轉換成數值目標 (NT) 的規則：  
  
1.  將 CS 取代為在 CS 中移除任何前置或尾端空格所取得的值。 如果 CS 不是有效的 *數值常*值，就會傳回 SQLSTATE 22018 (轉換規格) 的無效字元值。  
  
2.  將 CS 取代為取得的值，方法是移除小數點之前的前置零、小數點後的尾端零，或兩者。  
  
3.  將 CS 轉換為 NT。 如果轉換導致遺失有效位數，則會傳回 SQLSTATE 22003 (值超出範圍) 。 如果轉換造成 nonsignificant 位數遺失，則會傳回 SQLSTATE 01S07 (小數截斷) 。  
  
## <a name="numeric-source-to-character-target"></a>數值來源到字元目標  
 以下是從數值來源 (NS) 轉換成字元目標 (CT) 的規則：  
  
1.  讓 LT 成為 CT 的字元長度。 針對抓取指派，LT 等於緩衝區的長度（以字元為單位），而不是這個字元集的 null 終止字元中的位元組數目。  
  
2.  例：  
  
    -   如果 NS 是精確的數值型別，則讓 YP 等於最短的字元字串，該字串符合 *精確數值常* 值的定義，因此 YP 的小數位數與 ns 的小數位數相同，而 YP 的解讀值是 ns 的絕對值。  
  
    -   如果 NS 是近似的數數值型別，則讓 YP 成為字元字串，如下所示：  
  
         案例：  
  
         如果 NS 等於0，則 YP 為0。  
  
         讓 YSN 成為最短的字元字串，其符合精確*數值常* 值的定義，而其轉譯值為 NS 的絕對值。 如果 YSN 的長度小於 NS 資料類型的 (*precision* + 1) ，則讓 YP 等於 YSN。  
  
         否則，YP 是最短的字元字串，該字串會符合 *近似數值常* 值的定義，其解釋值為 NS 的絕對值，而其 *尾數* 包含不是 ' 0 ' 的單一 *數位* ，後面接著 *句號* 和不 *帶正負號的整數*。  
  
3.  案例：  
  
    -   如果 NS 小於0，則讓 Y 成為下列結果：  
  
         '-'  &#124;&#124; YP  
  
         其中 ' &#124;&#124; ' 是字串串連運算子。  
  
         否則，請讓 Y 等於 YP。  
  
4.  讓 LESSON.LY 成為 Y 的長度（以字元為單位）。  
  
5.  案例：  
  
    -   如果 LESSON.LY 等於 LT，則 [CT] 會設定為 [Y]。  
  
    -   如果 LESSON.LY 小於 LT，則會在適當的空間數目之後，將 CT 設定為右邊的 Y 擴充。  
  
         否則 (LESSON.LY > LT) ，請將 Y 的第一個 LT 字元複製到 CT 中。  
  
         案例：  
  
         如果這是存放區指派，則會傳回錯誤 SQLSTATE 22001 (字串資料，) 右截斷。  
  
         如果這是抓取指派，請傳回警告 SQLSTATE 01004 (字串資料，) 右截斷。 當複製產生的小數位數 (不超過尾端零) 時，它就是驅動程式自訂是否發生下列其中一種情況：  
  
          (1) 驅動程式會將 Y 中的字串截斷為適當的縮放 (，也可以是零) 並將結果寫入至 CT。  
  
          (2) 驅動程式會將 Y 中的字串四捨五入至適當的縮放 (，也可以是零) 並將結果寫入至 CT。  
  
          (3) 驅動程式不會截斷或四捨五入，而只會將 Y 的第一個 LT 字元複製到 CT。

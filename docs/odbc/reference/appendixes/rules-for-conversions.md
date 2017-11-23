---
title: "轉換規則 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- numeric data type [ODBC], literals
- conversions with numeric literals [ODBC]
- numeric literals [ODBC]
- literals [ODBC], numeric
ms.assetid: 89f846a3-001d-496a-9843-ac9c38dc1762
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 673b0a0ca903e5607822f78363c300f40a2df0ac
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="rules-for-conversions"></a>轉換規則
本節中的規則適用於包含數值常值轉換。 這些規則的目的，會定義下列詞彙：  
  
-   *儲存指派：*時將資料傳送到資料庫中的資料表資料行。 呼叫期間發生此錯誤**SQLExecute**， **SQLExecDirect**，和**SQLSetPos**。 在存放區指派 「 目標 」 是指資料庫資料行和 「 來源 」 是指應用程式緩衝區中的資料。  
  
-   *擷取指派：*若干應用程式緩衝區，從資料庫擷取資料時。 呼叫期間發生此錯誤**SQLFetch**， **SQLGetData**， **SQLFetchScroll**，和**SQLSetPos**。 在擷取指派 「 目標 」 是指應用程式緩衝區和 「 來源 」 是指資料庫資料行。  
  
-   *CS:*字元來源中的值。  
  
-   *NT:*數值目標中的值。  
  
-   *NS:*數值來源中的值。  
  
-   *CT:*字元目標中的值。  
  
-   確切的數值常值的有效位數： 它所包含的位數。  
  
-   確切的數字常值的小數位數： 的明示或默示期間的右邊的位數。  
  
-   近似的數值常值的有效位數： 其尾數的有效位數。  
  
## <a name="character-source-to-numeric-target"></a>數值目標字元來源  
 以下是將來源的字元 (CS) 轉換為數值目標 (NT) 的規則：  
  
1.  CS 取代取得 CS 中移除任何開頭或尾端空格的值。 如果不是有效 CS*數值常值*，就會傳回 SQLSTATE 22018 （無效的字元值轉換規格的）。  
  
2.  CS 取代取得藉由移除小數點，結尾的小數點，後面的零或同時前面的前置零的值。  
  
3.  NT 轉換成 CS。 如果轉換導致遺失有效位數，則會傳回 SQLSTATE 22003 （數值超出範圍）。 如果轉換導致遺失不重要的數字，SQLSTATE 01S07 （小數位數截斷） 會傳回。  
  
## <a name="numeric-source-to-character-target"></a>數值來源到目標字元  
 以下是將來自數值來源 (NS) 轉換的字元目標 (CT) 的規則：  
  
1.  可讓長期是以字元為單位的 CT.長度 擷取指派的 LT 等於緩衝區長度減去此字元集 null 結束字元位元組數目的字元。  
  
2.  案例：  
  
    -   如果 NS 是精確數值類型，然後讓 YP 等於最短的定義符合字元字串*精確數值常值*的小數位數 YP 等同於小數位數 NS、 且 YP 解譯的值是NS 絕對值。  
  
    -   如果 NS 近似數值類型，然後讓 YP 是字元字串，如下所示：  
  
         案例：  
  
         如果 NS 等於 0，YP 為 0。  
  
         可讓最短的字元字串，符合確切-定義 YSN*數值常值*且解譯的值 NS 絕對值。 如果 YSN 長度小於 (*精確度*+ 1) 的 NS 的資料類型，然後讓 YP 等於 YSN。  
  
         否則 YP 是最短的定義符合字元字串*近似數值常值*解譯其實 NS 和其絕對值*尾數*組成單一*位數*也就是不 '0'，後面接著*期間*和*不帶正負號整數*。  
  
3.  案例：  
  
    -   如果 NS 小於 0，然後讓 Y 是結果：  
  
         '-' &#124; &#124;YP  
  
         其中 ' &#124; &#124;' 是字串串連運算子。  
  
         否則，可讓等於 YP Y。  
  
4.  可讓 LY 是以字元為單位 Y 的長度。  
  
5.  案例：  
  
    -   如果 LY 等於 LT，CT 是設定為 Y。  
  
    -   如果 LY LT，然後 CT 是設定為 Y 擴充右邊適當數目的空格。  
  
         否則 (LY > LT)，將 Y 的第一個 LT 字元複製到 CT.  
  
         案例：  
  
         如果這是存放區指派時，會傳回錯誤 SQLSTATE 22001 （字串資料，向右截斷）。  
  
         如果這是擷取指派時，會傳回警告 SQLSTATE 01004 （字串資料，向右截斷）。 複製產生的小數點後數字 （非尾端的零） 中遺失，時，驅動程式定義是否發生下列其中一項：  
  
         （1） 驅動程式會截斷 Y 中的字串，以適當的規模 （這也可以是零），並將結果寫入至 CT.  
  
         （2） 驅動程式將四捨五入 Y 中的字串，以適當的規模 （這也可以是零），並將結果寫入至 CT.  
  
         （3） 驅動程式都不會截斷也不會四捨五入，但只會將 Y 的第一個 LT 字元複製到 CT.

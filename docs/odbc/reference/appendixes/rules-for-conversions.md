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
manager: craigg
ms.openlocfilehash: a3ecee500204303dfcbcd8e179b9cb9cb0a94bae
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47706096"
---
# <a name="rules-for-conversions"></a>轉換規則
在本節中的規則適用於包含數值常值轉換。 基於這些規則的目的，定義下列詞彙：  
  
-   *儲存 指派：* 時將資料傳送到資料庫中的資料表資料行。 這會發生在呼叫**SQLExecute**， **SQLExecDirect**，並**SQLSetPos**。 在存放區指派 「 目標 」 是指資料庫資料行並 「 來源 」 是指應用程式緩衝區中的資料。  
  
-   *擷取指派：* 時從資料庫擷取資料到應用程式的緩衝區。 這會發生在呼叫**SQLFetch**， **SQLGetData**， **SQLFetchScroll**，以及**SQLSetPos**。 在擷取指派 「 目標 」 是指應用程式緩衝區而 「 來源 」 是指資料庫資料行。  
  
-   *CS:* 字元來源中的值。  
  
-   *NT:* 數值目標中的值。  
  
-   *NS:* 數值來源中的值。  
  
-   *CT:* 字元目標中的值。  
  
-   確切的數值常值的有效位數： 它所包含的數字數目。  
  
-   確切的數值常值的小數位數： 之明示或默示的週期右邊的位數。  
  
-   近似的數值常值的有效位數： 其尾數的有效位數。  
  
## <a name="character-source-to-numeric-target"></a>數字的目標字元來源  
 以下是字元來源 (CS) 的轉換為數值的目標 (NT) 規則：  
  
1.  取得在 CS 中移除任何開頭或尾端空格的值取代 CS。 如果不是有效 CS*數值常值*，則會傳回 SQLSTATE 22018 （無效的字元值轉換規格的）。  
  
2.  CS 取代藉由移除前置的零，再小數點，結尾的小數點後的加上零，或兩者所取得的值。  
  
3.  轉換 NT CS。 如果轉換導致有效位數遺失，則會傳回 SQLSTATE 22003 （數值超出範圍）。 如果轉換導致遺失的重要數字，SQLSTATE 01S07 （小數位數截斷） 會傳回。  
  
## <a name="numeric-source-to-character-target"></a>字元目標的數值來源  
 以下是從數字的來源 (NS) 轉換成字元目標 (CT) 的規則：  
  
1.  讓是以字元為單位的 CT 長度 l 擷取指派的 l 等於緩衝區長度減去此字元集之 null 結束字元位元組數目的字元。  
  
2.  案例：  
  
    -   如果 NS 是精確數值類型，然後讓相等的定義符合的最短字元字串的 YP*確切的數值常值*使的小數位數 YP 等同的小數位數 NS，並且 YP 解譯值NS 的絕對值。  
  
    -   如果 NS 近似數值類型，然後讓 YP 是字元字串，如下所示：  
  
         案例：  
  
         如果 NS 等於 0，YP 就會是 0。  
  
         可讓要符合的確切-定義的最短字元字串的 YSN*數值常值*和其解譯的值是 NS 絕對值。 如果 YSN 長度小於 (*精確度*+ 1) 的 NS 的資料類型，然後讓 YP 等於 YSN。  
  
         否則 YP 是最短的定義符合的字元字串*近似數值常值*其解譯的值是數值的 NS 和其絕對值*尾數*組成單一*數字*也就是沒有 '0'，後面接著*期間*並*不帶正負號整數*。  
  
3.  案例：  
  
    -   如果 NS 小於 0，然後讓 Y 是結果：  
  
         '-' &AMP;#124; &AMP;#124; YP  
  
         位置 '&#124;&#124;' 是字串串連運算子。  
  
         否則，可讓等於 YP Y。  
  
4.  可讓 LY 是 Y 個字元的長度。  
  
5.  案例：  
  
    -   如果 LY 等於 l，CT 設為 Y。  
  
    -   如果 LY L，則 CT 會設定為 Y 擴充右側的適當數目的空格。  
  
         否則 (LY > L)，將 Y 的第一個 l 字元複製到 CT  
  
         案例：  
  
         如果這是存放區指派時，會傳回錯誤 SQLSTATE 22001 （字串資料右側截斷）。  
  
         如果這是擷取指派時，會傳回 SQLSTATE 01004 （字串資料右側截斷） 的警告。 複製結果的小數位數 （非尾端的零） 中遺失，時，驅動程式定義是否會發生下列其中一項：  
  
         （1） 驅動程式會截斷 （這也可以是零） 的適當調整 Y 中的字串，並將結果寫入至 CT  
  
         （2） 驅動程式將四捨五入 Y 中的字串，以適當的規模 （這也可以是零），並將結果寫入至 CT  
  
         （3） 驅動程式都不會截斷或四捨五入，但只是將 Y 的第一個 l 字元複製到 CT

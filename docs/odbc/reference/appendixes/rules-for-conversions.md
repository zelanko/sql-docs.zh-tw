---
title: 轉換規則 |微軟文件
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
ms.openlocfilehash: c49177d62fffc3b3b5c47a25bf3fb421d7564245
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305084"
---
# <a name="rules-for-conversions"></a>轉換規則
本節中的規則適用於涉及數位文本的轉換。 就這些規則而言,定義了以下術語:  
  
-   *儲存配置:* 將數據發送到資料庫中的表列時。 這發生在對**SQLExecute、SQLExecDirect****和**的調**SQLExecDirect**用期間。 在存儲分配期間,"目標"是指資料庫列,"源"是指應用程序緩衝區中的數據。  
  
-   *檢索配置:* 將數據從資料庫檢索到應用程式緩衝區時。 這發生在對**SQLFetch、SQLGetData、SQLFetchScroll**和**SQLSetPos**的**SQLFetch****SQLFetchScroll**調用期間。 在檢索分配期間,「目標」是指應用程式緩衝區,「源」是指資料庫列。  
  
-   *CS:* 字元源中的值。  
  
-   *NT:* 數值目標中的值。  
  
-   *NS:* 數值源中的值。  
  
-   *CT:* 字元目標中的值。  
  
-   精確數字文本的精度:它包含的數字數。  
  
-   精確數位文本的刻度:明示或隱含期間右側的數字數。  
  
-   近似數位文本的精度:其曼蒂薩的精度。  
  
## <a name="character-source-to-numeric-target"></a>字元來源到數字目標  
 以下是從字元來源 (CS) 轉換為數字目標 (NT) 的規則:  
  
1.  將 CS 替換為透過刪除 CS 中的任何前導空格或尾隨空格而獲得的值。 如果 CS 不是有效的*數位文本*,則傳回 SQLSTATE 22018(強制轉換規範的無效字元值)。  
  
2.  將 CS 替換為通過刪除小數點前的前導零、在小數點之後尾隨零或兩者兩者,獲得的值。  
  
3.  將 CS 轉換為 NT。 如果轉換導致重要數位丟失,則返回 SQLSTATE 22003(數值範圍外)。 如果轉換導致非有效數位丟失,則返回 SQLSTATE 01S07(分數截斷)。  
  
## <a name="numeric-source-to-character-target"></a>數位來源到字元目標  
 以下是從數位源 (NS) 轉換為字元目標 (CT) 的規則:  
  
1.  讓 LT 以 CT 字元表示長度。 對於檢索賦值,LT 等於字元中的緩衝區長度減去此字元集的 null 終止字元中的位元組數。  
  
2.  例:  
  
    -   如果 NS 是精確數值類型,則讓 YP 等於符合*精確數位文本*定義的最短字串,以便 YP 的比例與 NS 的比例相同,而 YP 的解釋值是 NS 的絕對值。  
  
    -   如果 NS 是近似數值類型,則讓 YP 成為字串,如下所示:  
  
         案例：  
  
         如果 NS 等於 0,則 YP 為 0。  
  
         讓 YSN 成為符合精確*數位文本*定義的最短字串,其解釋值是 NS 的絕對值。 如果 YSN 的長度小於 NS 資料類型的 (*精度*= 1),則讓 YP 等於 YSN。  
  
         否則,YP 是符合*近似數位文本*定義的最短字串,其解釋值是 NS 的絕對值,其*符號*由不是"0"的單個*數位*組成,後跟句*點*和無*符號整數*。  
  
3.  案例：  
  
    -   如果 NS 小於 0,則讓 Y 成為以下結果:  
  
         '-' &#124;&#124; YP  
  
         其中「&#124;&#124;」是字串串聯運算元。  
  
         否則,讓 Y 等於 YP。  
  
4.  讓 LY 以 Y 字元的長度。  
  
5.  案例：  
  
    -   如果 LY 等於 LT,則 CT 設置為 Y。  
  
    -   如果 LY 小於 LT,則 CT 按適當數量的空格在右側設置為 Y 擴展。  
  
         否則(LY > LT),將 Y 的第一個 LT 字元複製到 CT 中。  
  
         案例：  
  
         如果這是存儲分配,則返回錯誤 SQLSTATE 22001(字串數據,右截斷)。  
  
         如果這是檢索分配,則返回警告 SQLSTATE 01004(字串數據,右截斷)。 當複製導致小數位數丟失(尾隨零以外的)時,驅動程式定義是否發生以下情況之一:  
  
         (1) 驅動程式將 Y 中的字串截截到適當的比例(也可以為零),並將結果寫入 CT。  
  
         (2) 驅動程式將 Y 中的字串舍入到適當的比例(也可以為零),並將結果寫入 CT。  
  
         (3) 驅動程式既不截流也不轉,只需將 Y 的第一個 LT 字元複製到 CT 中。

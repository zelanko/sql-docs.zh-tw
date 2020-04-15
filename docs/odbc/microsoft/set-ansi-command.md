---
title: 設定 ANSI 指令 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- set ANSI command [ODBC]
ms.assetid: cf9a01b2-14bf-458c-a73c-2a58ddef32d8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 97269642b4147b966fdd71003f5f81ebe7905282
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300908"
---
# <a name="set-ansi-command"></a>SET ANSI 命令
確定如何使用 Visual FoxPro SQL 指令中的 # 運算元對不同長度的字串進行比較。  
  
## <a name="syntax"></a>語法  
  
```  
  
SET ANSI ON | OFF  
```  
  
## <a name="arguments"></a>引數  
 開啟  
 (驅動程式的預設值;Visual FoxPro 的預設值為 OFF。用使長度等於較長字串長度所需的空白填充較短的字串。 然後,將兩個字串的字元與其整個長度的字元進行比較。 請考慮此比較:  
  
```  
'Tommy' = 'Tom'  
```  
  
 結果是 False (。F.) 如果 SET ANSI 處於打開,因為當填充時,"Tom"變為"湯姆",字串"湯姆"和"Tommy"與字元不匹配。  
  
 在 Visual FoxPro SQL 命令中,* 運算符使用此方法進行比較。  
  
 OFF  
 指定較短的字串不會用空格填充。 在到達較短的字串之前,將比較字元的兩個字串的字元。 請考慮此比較:  
  
```  
'Tommy' = 'Tom'  
```  
  
 結果為"為"(。T.) 當 SET ANSI 關閉時,因為比較在"Tom"之後停止。  
  
## <a name="remarks"></a>備註  
 SET ANSI 確定在進行 SQL 字串比較時,是否用空白填充兩個字串的較短時間。 SET ANSI 對 = 運算符沒有影響;使用 * 運算子時,較短的字串始終用空白填充以進行比較。  
  
## <a name="string-order"></a>字串順序  
 在 SQL 命令中,比較中兩個字串的從左到右順序不相關,將字串從 * 或 * 運算子的一側切換到另一側不會影響比較的結果。  
  
## <a name="see-also"></a>另請參閱  
 [選擇 - SQL 指令](../../odbc/microsoft/select-sql-command.md)   
 [SET EXACT 命令](../../odbc/microsoft/set-exact-command.md)

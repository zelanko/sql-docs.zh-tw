---
title: 設定 ANSI 命令 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300908"
---
# <a name="set-ansi-command"></a>SET ANSI 命令
決定如何使用 Visual FoxPro SQL 命令中的 = 運算子來建立不同長度之字串之間的比較。  
  
## <a name="syntax"></a>語法  
  
```  
  
SET ANSI ON | OFF  
```  
  
## <a name="arguments"></a>引數  
 開啟  
 （驅動程式的預設值; Visual FoxPro 的預設值為 OFF）。填補較短的字串，並將其設為等於較長字串長度所需的空白。 接著，兩個字串會針對其整個長度進行字元比較。 請考慮下列比較：  
  
```  
'Tommy' = 'Tom'  
```  
  
 結果為 False （。F.）如果 SET ANSI 是 on，因為在填補時，' Tom ' 會變成 ' Tom '，而字串 ' Tom ' 與 ' Tommy ' 不符合字元。  
  
 = = 運算子會使用這個方法，在 Visual FoxPro SQL 命令中進行比較。  
  
 OFF  
 指定不以空白填補較短的字串。 兩個字串會針對字元進行比較，直到到達較短字串的結尾為止。 請考慮下列比較：  
  
```  
'Tommy' = 'Tom'  
```  
  
 結果為 True （。T.）當 SET ANSI 為 off 時，因為比較會在 ' Tom ' 之後停止。  
  
## <a name="remarks"></a>備註  
 SET ANSI 決定在進行 SQL 字串比較時，兩個字串中較短的是否會以空白填補。 SET ANSI 不會影響 = = 運算子;當您使用 = = 運算子時，較短的字串一律會以空格填補以進行比較。  
  
## <a name="string-order"></a>字串順序  
 在 SQL 命令中，比較中兩個字串的由左至右順序會從 = 或 = 運算子的一端 irrelevantswitching 一個字串，而不會影響比較的結果。  
  
## <a name="see-also"></a>另請參閱  
 [SELECT-SQL 命令](../../odbc/microsoft/select-sql-command.md)   
 [SET EXACT 命令](../../odbc/microsoft/set-exact-command.md)

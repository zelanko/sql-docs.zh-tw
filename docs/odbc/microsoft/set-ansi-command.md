---
title: SET ANSI 命令 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5af98bd8f16d7278b932ad89f1c81c58ddb1fb54
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63127869"
---
# <a name="set-ansi-command"></a>SET ANSI 命令
判斷如何比較不同長度的字串之間進行與 = Visual FoxPro SQL 命令中的運算子。  
  
## <a name="syntax"></a>語法  
  
```  
  
SET ANSI ON | OFF  
```  
  
## <a name="arguments"></a>引數  
 ON  
 （預設驅動程式; Visual FoxPro 的預設值是 OFF）。較短的字串，含有空白所需的填補讓等於更長的字串長度。 這兩個字串則比較其整個長度的字元的字元。 這項比較，請考慮：  
  
```  
'Tommy' = 'Tom'  
```  
  
 結果為 False (。F.) 如果設定 ANSI 已開啟，因為當填補時，'Tom' 變成 'Tom' 和 'Tom' 和 'Tommy' 字串不相符的字元的字元。  
  
 = = 運算子會使用這個方法來比較 Visual FoxPro SQL 命令中。  
  
 OFF  
 指定以空白不填較短的字串。 比較兩個字串的字元，直到達到較短的字串結尾的字元。 這項比較，請考慮：  
  
```  
'Tommy' = 'Tom'  
```  
  
 結果為 True (。T.） 時設定的 ANSI 已關閉，因為比較之後就會停止 'Tom'。  
  
## <a name="remarks"></a>備註  
 設定 ANSI 決定是否在較短的兩個字串填補以空白的 SQL 字串比較時。 並不會影響設定的 ANSI = = 運算子;當您使用 = = 運算子，較短的字串一律會填補以空白進行比較。  
  
## <a name="string-order"></a>字串順序  
 在 SQL 命令中，由左到右的順序來比較兩個字串是 irrelevantswitching 字串從一端 = 或 = = 運算子之間並不會影響比較的結果。  
  
## <a name="see-also"></a>另請參閱  
 [SELECT-SQL 命令](../../odbc/microsoft/select-sql-command.md)   
 [SET EXACT 命令](../../odbc/microsoft/set-exact-command.md)

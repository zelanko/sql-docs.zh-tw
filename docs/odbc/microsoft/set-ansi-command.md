---
title: SET ANSI 命令 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- set ANSI command [ODBC]
ms.assetid: cf9a01b2-14bf-458c-a73c-2a58ddef32d8
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b713588ba8140b74f19ccb1e9a90b1fa1949754a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="set-ansi-command"></a>SET ANSI 命令
判斷如何比較不同長度的字串之間進行與 = Visual FoxPro SQL 命令中的運算子。  
  
## <a name="syntax"></a>語法  
  
```  
  
SET ANSI ON | OFF  
```  
  
## <a name="arguments"></a>引數  
 ON  
 （預設的驅動程式，Visual FoxPro 的預設值是 OFF）。以空白較短的字串所需的填補讓等於更長的字串長度。 兩個字串就比較的字元，其整個長度的字元。 這項比較，請考慮：  
  
```  
'Tommy' = 'Tom'  
```  
  
 結果為 False (。F.) 如果設定 ANSI 已開啟，因為當填補時，'Tom' 變成 'Tom' 和 'Tom' 和 'Tommy' 字串不相符的字元的字元。  
  
 = = 運算子會使用這個方法來比較 Visual FoxPro SQL 命令中。  
  
 OFF  
 指定不填補空格較短的字串。 比較兩個字串的字元，直到達到較短的字串結尾的字元。 這項比較，請考慮：  
  
```  
'Tommy' = 'Tom'  
```  
  
 結果為 True (。T） 時設定的 ANSI 已關閉，因為比較之後就會停止 'Tom'。  
  
## <a name="remarks"></a>備註  
 設定 ANSI 決定是否使用較短的兩個字串填補以空白進行 SQL 字串的比較時。 設定 ANSI 沒有任何作用 = = 運算子。當您使用 = = 運算子，較短的字串一律會填補以空白進行比較。  
  
## <a name="string-order"></a>字串順序  
 SQL 命令中左到右的順序來比較兩個字串是 irrelevantswitching 字串從一端的 = = = 或運算子之間並不會影響比較的結果。  
  
## <a name="see-also"></a>另請參閱  
 [選取的 SQL 命令](../../odbc/microsoft/select-sql-command.md)   
 [SET EXACT 命令](../../odbc/microsoft/set-exact-command.md)

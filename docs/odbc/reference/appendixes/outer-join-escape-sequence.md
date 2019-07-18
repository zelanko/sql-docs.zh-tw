---
title: 外部聯結逸出序列 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- outer join escape sequence [ODBC]
- escape sequences [ODBC], outer join
- ODBC escape sequences [ODBC], outer join
ms.assetid: 2cfd1525-6677-4d36-9b9e-730496853750
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 576fe7268ccf71a8c926f6b1124ebbf8a8c711b0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68100645"
---
# <a name="outer-join-escape-sequence"></a>外部聯結逸出序列
ODBC 會使用外部聯結逸出序列。 此逸出序列的語法如下所示：  
  
```  
{oj outer-join}  
```  
  
## <a name="remarks"></a>備註  
 在 backus-naur form，BNF 標記法中，語法如下所示：  
  
 *ODBC 外部-聯結的逸出*:: =  
  
 *ODBC-esc-啟動器*oj*外部聯結 ODBC esc 鍵結束字元*  
  
 *外部聯結*:: =*資料表名稱*[*相互關聯名稱*] {左&#124;權限&#124;完整}  
  
 外部聯結 {*資料表名稱*[*相互關聯名稱*] &#124; *外部聯結*} ON  
  
 *search-*  
  
 *條件*  
  
 *correlation-name* ::= *user-defined-name*  
  
 *起始 esc ODBC 端*:: = {  
  
 *ODBC esc 鍵結束字元*:: =}  
  
 若要判斷此陳述式的哪些部分支援，應用程式會呼叫**SQLGetInfo** SQL_OJ_CAPABILITIES 資訊類型。 外部聯結中，如*搜尋條件*必須包含只之間指定聯結條件*資料表名稱*。

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
manager: craigg
ms.openlocfilehash: ba08d33efca6fa90531f89bd57a307f42f343ebd
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47817643"
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
  
 *搜尋-*  
  
 *條件*  
  
 *相互關聯名稱*:: =*使用者定義名稱*  
  
 *起始 esc ODBC 端*:: = {  
  
 *ODBC esc 鍵結束字元*:: =}  
  
 若要判斷此陳述式的哪些部分支援，應用程式會呼叫**SQLGetInfo** SQL_OJ_CAPABILITIES 資訊類型。 外部聯結中，如*搜尋條件*必須包含只之間指定聯結條件*資料表名稱*。

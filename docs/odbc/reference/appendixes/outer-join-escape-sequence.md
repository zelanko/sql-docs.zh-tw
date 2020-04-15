---
title: 外部聯接轉義序列 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 37ce446328d263f492cdfd369f6e8f9f64fe6dfc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303609"
---
# <a name="outer-join-escape-sequence"></a>外部聯結逸出序列
ODBC 使用外部聯接的轉義序列。 此逸出序列的語法如下:  
  
```  
{oj outer-join}  
```  
  
## <a name="remarks"></a>備註  
 在 BNF 符號中,語法如下所示:  
  
 *ODBC-外部聯接轉義*::*  
  
 *ODBC-esc-開始器*oj*外部聯接 ODBC-esc 終結器*  
  
 *外部聯結*:::**表名*=*關聯名稱*[ 左&#124; 右 &#124; 完整]  
  
 外部聯接=*表名*=*關聯名稱*[ &#124;*外部連線*= 開啟  
  
 *搜尋-*  
  
 *條件*  
  
 *關聯名稱*::**使用者定義名稱*  
  
 *ODBC-esc -發物人*::*  
  
 *ODBC-esc 終結器*:*|  
  
 要確定支援此語句的哪些部分,應用程式使用SQL_OJ_CAPABILITIES資訊類型調用**SQLGetInfo。** 對於外部聯接,*搜索條件*必須僅包含指定*表名*之間的聯接條件。

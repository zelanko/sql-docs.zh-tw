---
title: 外部聯結 Escape 序列 |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68100645"
---
# <a name="outer-join-escape-sequence"></a>外部聯結逸出序列
ODBC 會使用外部聯結的 escape 序列。 此 escape 序列的語法如下：  
  
```  
{oj outer-join}  
```  
  
## <a name="remarks"></a>備註  
 在 BNF 標記法中，語法如下所示：  
  
 *ODBC-外部-聯結-escape* ：： =  
  
 *ODBC-esc-啟動器*oj*外部聯結 ODBC-esc-結束字元*  
  
 *outer-join* ：： =*資料表名稱*[相互*關聯名稱*] {LEFT &#124; RIGHT &#124; FULL}  
  
 外部聯結 {*資料表名稱*[相互*關聯名稱*] &#124;*外部聯結*} 開啟  
  
 *search*  
  
 *條件*  
  
 相互*關聯名稱*：： =*使用者定義名稱*  
  
 *ODBC-esc-啟動器*：： = {  
  
 *ODBC-esc-結束字元*：： =}  
  
 為了判斷支援此語句的哪些部分，應用程式會使用 SQL_OJ_CAPABILITIES 資訊類型來呼叫**SQLGetInfo** 。 對於外部聯結，*搜尋條件*必須只包含指定之*資料表名稱*之間的聯結條件。

---
description: 外部聯結逸出序列
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 22517e676f9f8ac80622d368edcdb5a0ce1b283f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466090"
---
# <a name="outer-join-escape-sequence"></a>外部聯結逸出序列
ODBC 針對外部聯結使用 escape 序列。 此 escape 順序的語法如下所示：  
  
```  
{oj outer-join}  
```  
  
## <a name="remarks"></a>備註  
 在 BNF 標記法中，語法如下所示：  
  
 *ODBC-outer-join-escape* ：： =  
  
 *ODBC-esc-啟動器* oj *外部聯結 ODBC-esc-結束字元*  
  
 *外部聯結* ：： = *資料表名稱* [相互*關聯-名稱*] {LEFT &#124; RIGHT &#124; FULL}  
  
 外部聯結 {*資料表名稱* [相互*關聯-名稱*] &#124; *外部聯結*} 開啟  
  
 *查詢*  
  
 *條件*  
  
 相互*關聯-名稱*：： =*使用者定義的名稱*  
  
 *ODBC-esc-啟動器* ：： = {  
  
 *ODBC-esc-結束字元* ：： =}  
  
 為了判斷支援此語句的部分，應用程式會使用 SQL_OJ_CAPABILITIES 資訊類型來呼叫 **SQLGetInfo** 。 若為外部聯結， *搜尋條件* 必須只包含指定之 *資料表名稱*之間的聯結條件。

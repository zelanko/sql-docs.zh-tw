---
title: LIKE 逸出序列 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC escape sequences [ODBC], LIKE
- LIKE escape sequence [ODBC]
- escape sequences [ODBC], LIKE
ms.assetid: 798d75ea-be9d-4bef-b297-318bc327f1ca
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 65447904f32b7e0457ed807f18e942b334ddc236
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47626616"
---
# <a name="like-escape-sequence"></a>LIKE 逸出序列
ODBC 會將逸出序列用於 LIKE 子句。 此逸出序列的語法如下所示：  
  
```  
{'escape-character'}  
```  
  
## <a name="remarks"></a>備註  
 在 backus-naur form，BNF 標記法中，語法如下所示：  
  
 *ODBC like 逸出*:: =  
  
 *ODBC-esc-啟動器*逸出 '*逸出字元*' *ODBC esc 鍵結束字元*  
  
 *逸出字元*:: =*字元*  
  
 *起始 esc ODBC 端*:: = {  
  
 *ODBC esc 鍵結束字元*:: =}  
  
 若要判斷驅動程式是否支援 LIKE 逸出序列，應用程式可以呼叫**SQLGetInfo** SQL_LIKE_ESCAPE_CLAUSE 資訊類型。

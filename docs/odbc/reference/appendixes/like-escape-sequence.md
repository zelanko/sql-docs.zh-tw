---
title: 要逸出序列 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC escape sequences [ODBC], LIKE
- LIKE escape sequence [ODBC]
- escape sequences [ODBC], LIKE
ms.assetid: 798d75ea-be9d-4bef-b297-318bc327f1ca
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 37733aadb069cd161427fc8f186647cfba030b6d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32906503"
---
# <a name="like-escape-sequence"></a>要逸出序列
ODBC 會逸出序列使用 LIKE 子句。 此逸出序列語法如下所示：  
  
```  
{'escape-character'}  
```  
  
## <a name="remarks"></a>備註  
 在 BNF 標記法，語法如下所示：  
  
 *ODBC 類似-逸出*:: =  
  
 *起始 esc ODBC 端*逸出 '*逸出字元*' *ODBC esc 結束字元*  
  
 *逸出字元*:: =*字元*  
  
 *起始 esc ODBC 端*:: = {  
  
 *ODBC esc 結束字元*:: =}  
  
 若要判斷驅動程式是否支援 LIKE 逸出序列，應用程式可以呼叫**SQLGetInfo** SQL_LIKE_ESCAPE_CLAUSE 資訊類型。

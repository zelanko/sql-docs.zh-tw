---
title: 喜歡轉義序列 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 517c21f7b64fa7ceb662af9839a9fed1a1e6eff6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304919"
---
# <a name="like-escape-sequence"></a>LIKE 逸出序列
ODBC 使用 LIKE 子句的轉義序列。 此逸出序列的語法如下:  
  
```  
{'escape-character'}  
```  
  
## <a name="remarks"></a>備註  
 在 BNF 符號中,語法如下所示:  
  
 *ODBC 類似轉義*::*  
  
 *ODBC-esc-發端器*逃生'*逃生字元**'ODBC-esc終結器*  
  
 *轉義字元*::**字元*  
  
 *ODBC-esc -發物人*::*  
  
 *ODBC-esc 終結器*:*|  
  
 要確定驅動程式是否支援 LIKE 轉義序列,應用程式可以使用SQL_LIKE_ESCAPE_CLAUSE資訊類型調用**SQLGetInfo。**

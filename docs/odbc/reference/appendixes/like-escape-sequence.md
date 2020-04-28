---
title: LIKE Escape 序列 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304919"
---
# <a name="like-escape-sequence"></a>LIKE 逸出序列
ODBC 會針對 LIKE 子句使用 escape 序列。 此 escape 序列的語法如下：  
  
```  
{'escape-character'}  
```  
  
## <a name="remarks"></a>備註  
 在 BNF 標記法中，語法如下所示：  
  
 *類似 ODBC 的-escape* ：： =  
  
 *Odbc-esc-啟動器*escape '*escape-字元*' *ODBC-esc-結束字元*  
  
 *escape 字元*：： =*字元*  
  
 *ODBC-esc-啟動器*：： = {  
  
 *ODBC-esc-結束字元*：： =}  
  
 若要判斷驅動程式是否支援 LIKE 逸出序列，應用程式可以使用 SQL_LIKE_ESCAPE_CLAUSE 資訊類型來呼叫**SQLGetInfo** 。

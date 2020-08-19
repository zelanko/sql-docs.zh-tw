---
description: LIKE 逸出序列
title: LIKE Escape Sequence |Microsoft Docs
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
ms.openlocfilehash: 19d20f80f9fea4df2c508ec4ec4bcc2ee6718986
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429640"
---
# <a name="like-escape-sequence"></a>LIKE 逸出序列
ODBC 針對 LIKE 子句使用 escape 序列。 此 escape 順序的語法如下所示：  
  
```  
{'escape-character'}  
```  
  
## <a name="remarks"></a>備註  
 在 BNF 標記法中，語法如下所示：  
  
 *類似 ODBC 的-escape* ：： =  
  
 *Odbc-esc-啟動器* escape '*escape-character*' *ODBC-esc-結束字元*  
  
 *escape 字元* ：： = *字元*  
  
 *ODBC-esc-啟動器* ：： = {  
  
 *ODBC-esc-結束字元* ：： =}  
  
 若要判斷驅動程式是否支援 LIKE escape 序列，應用程式可以使用 SQL_LIKE_ESCAPE_CLAUSE 資訊類型來呼叫 **SQLGetInfo** 。

---
title: 純量函數 Escape 序列 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC], scalar function
- scalar functions [ODBC], escape sequences
- ODBC escape sequences [ODBC], scalar function
ms.assetid: aaf5d516-e090-445f-8839-9e39581c69c7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8347b8e6f0fab6dffc5295fb3b8260a6a56ed123
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305071"
---
# <a name="scalar-function-escape-sequence"></a>純量函式逸出序列
ODBC 會針對純量函數使用 escape 序列。 此 escape 序列的語法如下：  
  
```  
{fn scalar-function}  
```  
  
## <a name="remarks"></a>備註  
 在 BNF 標記法中，語法如下所示：  
  
 *ODBC-純量函數-escape* ：： =  
  
 *ODBC-esc-啟動器*fn 純量*函數 ODBC-esc-結束字元*  
  
 純量*函數*：： =*函數名稱*（*引數清單*）  
  
 （非終端項函*式名稱*和函*式名稱*（*引數清單*）的定義衍生自[附錄 E：](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)純量函數中的純量函數清單）。  
  
 *ODBC-esc-啟動器*：： = {  
  
 *ODBC-esc-結束字元*：： =}  
  
 若要判斷資料來源是否支援程式，而且該驅動程式支援 ODBC 程序呼叫語法，應用程式可以呼叫**SQLGetInfo**。 如需詳細資訊，請參閱[附錄 E：](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)純量函數。

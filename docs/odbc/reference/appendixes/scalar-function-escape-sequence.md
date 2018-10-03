---
title: 純量函式逸出序列 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0913458d683d7641145b262552e147033dbfc054
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47660786"
---
# <a name="scalar-function-escape-sequence"></a>純量函式逸出序列
ODBC 純量函式使用逸出序列。 此逸出序列的語法如下所示：  
  
```  
{fn scalar-function}  
```  
  
## <a name="remarks"></a>備註  
 在 backus-naur form，BNF 標記法中，語法如下所示：  
  
 *ODBC 純量-函式-逸出*:: =  
  
 *ODBC-esc-啟動器*fn*純量函數 ODBC esc 鍵結束字元*  
  
 *純量函數*:: =*函式名稱*(*引數清單*)  
  
 (非終端項的定義*函式名稱*並*函式名稱*(*引數清單*) 中的純量函數的清單來自[附錄 e： 純量函數](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)。)  
  
 *起始 esc ODBC 端*:: = {  
  
 *ODBC esc 鍵結束字元*:: =}  
  
 若要判斷資料來源支援程序及驅動程式支援 ODBC 的程序引動過程語法，應用程式可以呼叫**SQLGetInfo**。 如需詳細資訊，請參閱 <<c0> [ 附錄 e： 純量函式](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)。

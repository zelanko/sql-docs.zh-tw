---
title: Scalar 函數轉義序列 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305071"
---
# <a name="scalar-function-escape-sequence"></a>純量函式逸出序列
ODBC 使用轉義序列進行標量函數。 此逸出序列的語法如下:  
  
```  
{fn scalar-function}  
```  
  
## <a name="remarks"></a>備註  
 在 BNF 符號中,語法如下所示:  
  
 *ODBC-標點-功能轉義*::*  
  
 *ODBC-esc-開始器*fn*標量函數 ODBC-esc 終結器*  
  
 *標量函數*::**函式名稱*(*參數清單*)  
  
 ( 非終端*函數名稱*與*函數名稱*(*參數清單*)的定義派生自附錄 E 中的標量函數清單[:Scalar 函數](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)。  
  
 *ODBC-esc -發物人*::*  
  
 *ODBC-esc 終結器*:*|  
  
 要確定資料來源是否支援程序,驅動程式支援 ODBC 程序呼叫語法,應用程式可以呼叫**SQLGetInfo**。 有關詳細資訊,請參閱附錄[E:Scalar 函數](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)。

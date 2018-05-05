---
title: 純量函數逸出序列 |Microsoft 文件
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
- escape sequences [ODBC], scalar function
- scalar functions [ODBC], escape sequences
- ODBC escape sequences [ODBC], scalar function
ms.assetid: aaf5d516-e090-445f-8839-9e39581c69c7
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8ca98389b0279ded2aba487e2e3e0f6bbbe95e6b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="scalar-function-escape-sequence"></a>純量函數逸出序列
ODBC 純量函數會使用逸出序列。 此逸出序列語法如下所示：  
  
```  
{fn scalar-function}  
```  
  
## <a name="remarks"></a>備註  
 在 BNF 標記法，語法如下所示：  
  
 *ODBC 純量函式-escape* :: =  
  
 *起始 esc ODBC 端*fn*純量函數 ODBC esc 結束字元*  
  
 *純量函數*:: =*函式名稱*(*引數清單*)  
  
 (如非終端項定義*函式名稱*和*函式名稱*(*引數清單*) 衍生自的純量函數清單[附錄 e： 純量函數](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)。)  
  
 *起始 esc ODBC 端*:: = {  
  
 *ODBC esc 結束字元*:: =}  
  
 若要判斷資料來源支援程序及驅動程式支援 ODBC 的程序引動過程語法，應用程式可以呼叫**SQLGetInfo**。 如需詳細資訊，請參閱[附錄 e： 純量函式](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)。

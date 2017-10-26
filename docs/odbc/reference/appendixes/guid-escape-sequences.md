---
title: "GUID 逸出序列 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC escape sequences [ODBC], GUID
- escape sequences [ODBC], guid
- guid escape sequence [ODBC]
ms.assetid: 71d43ef9-4a31-493e-b9e0-f864e9ef3ce6
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d4ed6e517d9a8fa6f4c28c7b05541d36262df2a8
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="guid-escape-sequences"></a>GUID 逸出序列
ODBC 使用 GUID 常值的逸出序列。 此逸出序列語法如下所示：  
  
```  
{guid 'nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn'}  
```  
  
## <a name="remarks"></a>備註  
 在 BNF 標記法，語法如下所示：  
  
 *ODBC-guid 逸出*:: =  
     *啟動 esc ODBC 者 guid* '*guid 值*' *ODBC esc 結束字元*  
  
 *起始 esc ODBC 端*:: = {  
  
 *ODBC esc 結束字元*:: =}  
  
 *guid 值*:: =*時鐘低價值 guid 分隔符號時鐘中間值 guid 分隔符號時鐘高價值 guid 分隔符號時鐘 seq 值 guid 分隔節點值*  
  
 *guid 分隔符號*:: =-  
  
 *時鐘低價值*:: = *hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit*  
  
 *時鐘中間值*:: = *hex_digit hex_digit hex_digit hex_digit*  
  
 *時鐘高價值*:: = *hex_digit hex_digit hex_digit hex_digit*  
  
 *時鐘 seq 值*:: = *hex_digit hex_digit hex_digit hex_digit*  
  
 *時鐘節點值*:: = *hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit*  
  
 *hex_digit* :: = 0 &#124; 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9 &#124;A &#124;B &#124;&#124;&#124;&#124;F  
  
 GUID 資料類型支援資料來源所支援的 GUID 常值的逸出序列。 應用程式應該呼叫**SQLGetTypeInfo**來判斷是否支援此資料類型。


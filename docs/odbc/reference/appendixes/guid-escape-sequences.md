---
title: GUID Escape 序列 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC escape sequences [ODBC], GUID
- escape sequences [ODBC], guid
- guid escape sequence [ODBC]
ms.assetid: 71d43ef9-4a31-493e-b9e0-f864e9ef3ce6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 44907bfbd884bf361ce5f2ab8b3f6d8a247aba44
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306969"
---
# <a name="guid-escape-sequences"></a>GUID 逸出序列
ODBC 會使用適用于 GUID 常值的 escape 序列。 此 escape 序列的語法如下：  
  
```  
{guid 'nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn'}  
```  
  
## <a name="remarks"></a>備註  
 在 BNF 標記法中，語法如下所示：  
  
 *ODBC-guid-escape* ：： =  
     *ODBC-esc-啟動器 guid*'*guid-值*' *ODBC-esc-結束字元*  
  
 *ODBC-esc-啟動器*：： = {  
  
 *ODBC-esc-結束字元*：： =}  
  
 *guid-value* ：： =*時鐘-低值 guid-分隔符號時鐘-中間值 guid-分隔符號時鐘-高值 guid-分隔符號時鐘-seq-值 guid-分隔符號節點-值*  
  
 *guid-separator* ：： =-  
  
 *時鐘-低值*：： = *hex_digit hex_digit hex_digit hex_digit hex_digit* hex_digit hex_digit hex_digit  
  
 *時鐘-中間值*：： = *hex_digit hex_digit hex_digit hex_digit*  
  
 *時鐘-高值*：： = *hex_digit hex_digit hex_digit hex_digit*  
  
 *clock-seq-value* ：： = *hex_digit hex_digit hex_digit hex_digit*  
  
 *clock-node-value* ：： = *hex_digit hex_digit hex_digit hex_digit hex_digit* hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit  
  
 *hex_digit* ：： = 0 &#124; 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9 &#124; &#124; E &#124; F  
  
 如果資料來源支援 GUID 資料類型，則支援 GUID 常值 escape 序列。 應用程式應該呼叫**SQLGetTypeInfo**來判斷是否支援此資料類型。

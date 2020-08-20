---
description: GUID 逸出序列
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
ms.openlocfilehash: d7babe2d26c0e5f2b311f8df5bbd1763622f3042
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466154"
---
# <a name="guid-escape-sequences"></a>GUID 逸出序列
ODBC 會針對 GUID 常值使用 escape 序列。 此 escape 順序的語法如下所示：  
  
```  
{guid 'nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn'}  
```  
  
## <a name="remarks"></a>備註  
 在 BNF 標記法中，語法如下所示：  
  
 *ODBC-guid-escape* ：： =  
     *ODBC-esc-啟動器 guid* '*guid-value*' *ODBC-esc-結束字元*  
  
 *ODBC-esc-啟動器* ：： = {  
  
 *ODBC-esc-結束字元* ：： =}  
  
 *guid-value* ：： = *時鐘-低值 guid-分隔符號時鐘-中間值 guid-分隔符號時鐘-高值 guid-分隔符號時鐘-seq-值 guid-分隔符號節點-值*  
  
 *guid-分隔符號* ：： =-  
  
 *時鐘-低-值*：： = *hex_digit hex_digit hex_digit hex_digit hex_digit* hex_digit hex_digit hex_digit  
  
 *時鐘中間值* ：： = *hex_digit hex_digit hex_digit hex_digit*  
  
 *時鐘-高-值* ：： = *hex_digit hex_digit hex_digit hex_digit*  
  
 *時鐘-seq-value* ：： = *hex_digit hex_digit hex_digit hex_digit*  
  
 *時鐘節點-值*：： = *hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit* hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit  
  
 *hex_digit* ：： = 0 &#124; 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; &#124; &#124; &#124; B &#124; C &#124; D &#124; E F  
  
 如果資料來源支援 GUID 資料類型，則支援 GUID 常值 escape 序列。 應用程式應該呼叫 **SQLGetTypeInfo** 來判斷是否支援此資料類型。

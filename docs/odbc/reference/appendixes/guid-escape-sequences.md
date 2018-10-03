---
title: GUID 逸出序列 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bf41671abc6393a18fad06e1debd297fed1f04c5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47654978"
---
# <a name="guid-escape-sequences"></a>GUID 逸出序列
ODBC 會將逸出序列用於 GUID 常值。 此逸出序列的語法如下所示：  
  
```  
{guid 'nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn'}  
```  
  
## <a name="remarks"></a>備註  
 在 backus-naur form，BNF 標記法中，語法如下所示：  
  
 *ODBC guid 逸出*:: =  
     *啟動 esc ODBC 者 guid* '*guid 值*' *ODBC esc 鍵結束字元*  
  
 *起始 esc ODBC 端*:: = {  
  
 *ODBC esc 鍵結束字元*:: =}  
  
 *guid 值*:: =*時鐘低價值 guid 分隔符號時脈中間值的 guid 分隔符號時鐘高價值的 guid 分隔符號時脈 seq 值 guid 分隔節點值*  
  
 *guid 分隔符號*:: =-  
  
 *時鐘低價值*:: = *hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit*  
  
 *時脈中間值*:: = *hex_digit hex_digit hex_digit hex_digit*  
  
 *時鐘高價值*:: = *hex_digit hex_digit hex_digit hex_digit*  
  
 *時脈 seq 值*:: = *hex_digit hex_digit hex_digit hex_digit*  
  
 *時鐘節點值*:: = *hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit*  
  
 *hex_digit* :: = 0 &#124; 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9 &#124; A &#124; B &#124; C &#124; D &#124; E &#124; F  
  
 如果資料來源所支援 GUID 資料類型，則，支援 GUID 常值的逸出序列。 應用程式應該呼叫**SQLGetTypeInfo**來判斷是否支援此資料型別。

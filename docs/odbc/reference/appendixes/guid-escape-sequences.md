---
title: GUID 逸出序列 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306969"
---
# <a name="guid-escape-sequences"></a>GUID 逸出序列
ODBC 使用轉義序列進行 GUID 文本。 此逸出序列的語法如下:  
  
```  
{guid 'nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn'}  
```  
  
## <a name="remarks"></a>備註  
 在 BNF 符號中,語法如下所示:  
  
 *ODBC-guid 轉義*::*  
     *ODBC-esc-開始器 guid*'*吉德值*' *ODBC-esc 終結器*  
  
 *ODBC-esc -發物人*::*  
  
 *ODBC-esc 終結器*:*|  
  
 *guid 值*::: =*時鐘-低值 guid-分隔符時鐘-中間值 guid-分隔符-高值 guid-分離器時鐘-值 guid-分離器節點值*  
  
 *吉德分離器*::* -  
  
 *時鐘低值*::* *hex_digit hex_digithex_digit hex_digithex_digithex_digit hex_digithex_digithex_digithex_digithex_digit*  
  
 *時鐘中間值*::* *hex_digithex_digithex_digithex_digit*  
  
 *時鐘高值*::* *hex_digithex_digithex_digithex_digit*  
  
 *時鐘-seq 值*::* *hex_digithex_digithex_digithex_digit*  
  
 *時鐘節點值*::* *hex_digithex_digithex_digit hex_digit hex_digithex_digit hex_digit hex_digithex_digithex_digithex_digithex_digithex_digithex_digithex_digit*  
  
 *hex_digit* ::* 0 &#124; 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9 &#124; a &#124; B &#124; C &#124; &#124; E &#124; F  
  
 如果資料來源支援 GUID 資料類型,則支援 GUID 文本轉義序列。 應用程式應呼叫**SQLGetTypeInfo**以確定是否支援此資料類型。

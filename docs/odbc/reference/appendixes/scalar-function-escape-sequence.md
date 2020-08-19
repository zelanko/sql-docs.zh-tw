---
description: 純量函式逸出序列
title: 純量函式 Escape 序列 |Microsoft Docs
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
ms.openlocfilehash: b00be53fa0b9e23c2ee2b4e9cbac2db8e9884bc7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424940"
---
# <a name="scalar-function-escape-sequence"></a>純量函式逸出序列
ODBC 會針對純量函數使用 escape 序列。 此 escape 順序的語法如下所示：  
  
```  
{fn scalar-function}  
```  
  
## <a name="remarks"></a>備註  
 在 BNF 標記法中，語法如下所示：  
  
 *ODBC-純量函數-escape* ：： =  
  
 *ODBC-esc-啟動器* fn 純量 *函數 ODBC-esc-結束字元*  
  
 純量*函數*：： = 函*式名稱* (*引數-清單*)   
  
  (非終端項函 *式名稱* 和函 *式名稱* (*引數清單*) 的定義衍生自 [附錄 E：](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)純量函式的純量函數清單。 )   
  
 *ODBC-esc-啟動器* ：： = {  
  
 *ODBC-esc-結束字元* ：： =}  
  
 若要判斷資料來源是否支援程式，以及驅動程式是否支援 ODBC 程序呼叫語法，應用程式可以呼叫 **SQLGetInfo**。 如需詳細資訊，請參閱 [附錄 E：](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)純量函數。

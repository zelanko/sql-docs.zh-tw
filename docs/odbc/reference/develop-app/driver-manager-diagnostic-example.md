---
description: 驅動程式管理員診斷範例
title: 驅動程式管理員診斷範例 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver manager [ODBC], diagnostic messages
- diagnostic information [ODBC], examples
- error messages [ODBC], diagnostic messages
ms.assetid: af8f2d35-d1bf-495c-af25-630654542b7d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b1d852436600ffb3ce5258e731d23c4579bf8964
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483061"
---
# <a name="driver-manager-diagnostic-example"></a>驅動程式管理員診斷範例
驅動程式管理員也可以產生診斷訊息。 例如，如果應用程式將不正確方向選項傳遞至 **SQLDataSources**，驅動程式管理員可能會格式化，並從 **SQLGetDiagRec**傳回下列值：  
  
```  
SQLSTATE:         "HY103"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Driver Manager]Direction option out of range"  
```  
  
 因為驅動程式管理員中發生此錯誤，所以它會在其廠商的診斷訊息中新增前置詞 ( [Microsoft] ) 與其識別碼 ( [ODBC 驅動程式管理員] ) 。

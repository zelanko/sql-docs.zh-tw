---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6ad253c2d0603846d6d1f795f6115e7bb727b3da
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47778572"
---
# <a name="driver-manager-diagnostic-example"></a>驅動程式管理員診斷範例
驅動程式管理員也可以產生診斷訊息。 例如，如果應用程式傳遞的不正確的方向選項**SQLDataSources**，驅動程式管理員可能會格式化，並傳回下列值從**SQLGetDiagRec**:  
  
```  
SQLSTATE:         "HY103"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Driver Manager]Direction option out of range"  
```  
  
 在驅動程式管理員發生錯誤，因為它加入前置詞診斷訊息 ([Microsoft]) 其供應商和它的識別項 （[ODBC 驅動程式管理員]）。

---
title: "驅動程式管理員診斷範例 |Microsoft 文件"
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
- driver manager [ODBC], diagnostic messages
- diagnostic information [ODBC], examples
- error messages [ODBC], diagnostic messages
ms.assetid: af8f2d35-d1bf-495c-af25-630654542b7d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3f373fe012c2b791329fea35ca853021e70274eb
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="driver-manager-diagnostic-example"></a>驅動程式管理員診斷範例
驅動程式管理員也可以產生診斷訊息。 例如，如果應用程式傳遞至無效的傳遞方向選項**SQLDataSources**，驅動程式管理員可能會格式化，並傳回下列值從**SQLGetDiagRec**:  
  
```  
SQLSTATE:         "HY103"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Driver Manager]Direction option out of range"  
```  
  
 在驅動程式管理員發生錯誤，因為它加入前置詞診斷訊息供應商 ([Microsoft]) 和其識別項 （[ODBC 驅動程式管理員]）。

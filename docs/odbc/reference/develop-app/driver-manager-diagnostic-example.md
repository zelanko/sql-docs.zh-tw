---
title: "驅動程式管理員診斷範例 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- driver manager [ODBC], diagnostic messages
- diagnostic information [ODBC], examples
- error messages [ODBC], diagnostic messages
ms.assetid: af8f2d35-d1bf-495c-af25-630654542b7d
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d51a5318c1b331a99ff1b108a3a56010a5e83a5b
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="driver-manager-diagnostic-example"></a>驅動程式管理員診斷範例
驅動程式管理員也可以產生診斷訊息。 例如，如果應用程式傳遞至無效的傳遞方向選項**SQLDataSources**，驅動程式管理員可能會格式化，並傳回下列值從**SQLGetDiagRec**:  
  
```  
SQLSTATE:         "HY103"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Driver Manager]Direction option out of range"  
```  
  
 在驅動程式管理員發生錯誤，因為它加入前置詞診斷訊息供應商 ([Microsoft]) 和其識別項 （[ODBC 驅動程式管理員]）。

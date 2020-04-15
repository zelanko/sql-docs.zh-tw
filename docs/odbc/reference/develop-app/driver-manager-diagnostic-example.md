---
title: 驅動程式管理員診斷範例 |微軟文件
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
ms.openlocfilehash: 839095e5544cab73cdddd4f4b17a3d8d52136c9c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305809"
---
# <a name="driver-manager-diagnostic-example"></a>驅動程式管理員診斷範例
驅動程式管理員還可以生成診斷消息。 例如,如果應用程式將無效的方向選項傳遞給**SQLDataSources,** 驅動程式管理員可能會格式化並從**SQLGetDiagRec 傳回**以下值 :  
  
```  
SQLSTATE:         "HY103"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Driver Manager]Direction option out of range"  
```  
  
 由於錯誤發生在驅動程式管理器中,因此它將首碼添加到其供應商 ([Microsoft]) 及其標識符 ([ODBC 驅動程式管理器])的診斷消息中。

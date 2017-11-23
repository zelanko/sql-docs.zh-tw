---
title: "使用精簡函式 |Microsoft 文件"
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
- concise functions [ODBC]
- functions [ODBC], concise functions
- descriptors [ODBC], concise functions
ms.assetid: 31ac070f-8c59-4fd5-bd5a-466bb27dbca0
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f58efc6ca7f6587ce7d7070bc02ad935efe06bff
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="using-concise-functions"></a>使用精簡函式
某些 ODBC 函數隱含存取描述元。 應用程式撰寫者可能會發現它們比撥號更方便**SQLSetDescField**或**SQLGetDescField**。 這些函式的呼叫*精簡*函式，因為它們執行的函式，包括設定或取得描述項欄位的數字。 某些精簡函式可讓應用程式設定或擷取單一函式呼叫中的數個相關的描述項欄位。  
  
 精簡函式可以呼叫未先擷取用來做為引數的描述項控制代碼。 這些函式使用的描述項欄位相關聯的陳述式控制代碼上呼叫。  
  
 精簡函式**SQLBindCol**和**SQLBindParameter**繫結資料行或參數對應的描述項欄位設為其引數。 所有這些函式會執行更多的工作比只要設定描述元。 **SQLBindCol**和**SQLBindParameter**提供完整的資料行或動態參數繫結的規格。 應用程式可以不過，變更個別的繫結的詳細資料，藉由呼叫**SQLSetDescField**或**SQLSetDescRec**並可以完全繫結資料行或參數藉由一系列的適當的呼叫這些函式。  
  
 精簡函式**SQLColAttribute**， **SQLDescribeCol**， **SQLDescribeParam**， **SQLNumParams**，和**SQLNumResultCols**擷取中的描述項欄位的值。  
  
 **SQLSetDescRec**和**SQLGetDescRec**精簡函式，一次呼叫，以設定或取得多個會影響的資料類型和資料行或參數資料的儲存體的描述項欄位。 **SQLSetDescRec**是要變更的資料行或參數的資料，在一個步驟中的繫結的有效方式。  
  
 **SQLSetStmtAttr**和**SQLGetStmtAttr**做為精簡函式，在某些情況下。 (請參閱[描述項欄位](../../../odbc/reference/develop-app/descriptor-fields.md)。)

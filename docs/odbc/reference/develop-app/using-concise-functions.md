---
title: 使用精簡函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- concise functions [ODBC]
- functions [ODBC], concise functions
- descriptors [ODBC], concise functions
ms.assetid: 31ac070f-8c59-4fd5-bd5a-466bb27dbca0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 43004601845d3032d404c308b7b1fa4850f694ee
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68022204"
---
# <a name="using-concise-functions"></a>使用精簡函式
有些 ODBC 函式隱含存取描述元。 應用程式撰寫者可能會發現它們比呼叫更方便**SQLSetDescField**或是**SQLGetDescField**。 這些函式會呼叫*精簡*函式，因為它們執行數項功能，包括設定或取得描述項欄位。 某些精簡函式可讓應用程式設定或擷取單一函式呼叫中的數個相關的描述項欄位。  
  
 精簡函式可以呼叫未先擷取做為引數的描述項控制代碼。 這些函式使用的描述項欄位相關聯的陳述式控制代碼上呼叫。  
  
 精簡函式**SQLBindCol**並**SQLBindParameter**繫結的資料行或參數對應的描述項欄位設為其引數。 所有這些函式會執行更多的工作比只要設定描述元。 **SQLBindCol**並**SQLBindParameter**提供完整的資料行或動態參數繫結的規格。 應用程式可以不過，藉由呼叫變更繫結的個別詳細資料**SQLSetDescField**或是**SQLSetDescRec**和可以藉由提出適合呼叫的一系列完整地結合資料行或參數這些函式。  
  
 精簡函式**SQLColAttribute**， **SQLDescribeCol**， **SQLDescribeParam**， **SQLNumParams**，和**SQLNumResultCols**擷取描述項欄位中的值。  
  
 **SQLSetDescRec**並**SQLGetDescRec**是精簡的函式，一次呼叫，以設定或取得多個會影響到儲存體的資料行或參數的資料與資料類型的描述項欄位。 **SQLSetDescRec**是要變更的資料行或參數的資料，在一個步驟中的繫結的有效方式。  
  
 **SQLSetStmtAttr**並**SQLGetStmtAttr**做為在某些情況下的精簡函式。 (請參閱[描述項欄位](../../../odbc/reference/develop-app/descriptor-fields.md)。)

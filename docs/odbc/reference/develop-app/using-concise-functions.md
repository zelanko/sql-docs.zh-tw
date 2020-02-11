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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68022204"
---
# <a name="using-concise-functions"></a>使用精簡函式
某些 ODBC 函式會取得描述項的隱含存取權。 應用程式寫入器可能會發現它們比呼叫**SQLSetDescField**或**SQLGetDescField**更方便。 這些函數稱為精簡函式，因為它們會執行*一些函數，* 包括設定或取得描述項欄位。 某些精簡的函式可讓應用程式在單一函式呼叫中設定或抓取數個相關的描述項欄位。  
  
 在不先抓取描述項控制碼做為引數使用的情況下，可以呼叫精簡的函式。 這些函式會使用與語句控制碼相關聯的描述項欄位，其會在其上呼叫。  
  
 精簡的函式**SQLBindCol**和**SQLBindParameter**會藉由設定對應至其引數的描述項欄位來系結資料行或參數。 這些函式中的每一個都會執行比單純設定描述項更多的工作。 **SQLBindCol**和**SQLBindParameter**提供資料行或動態參數之系結的完整規格。 不過，應用程式可以藉由呼叫**SQLSetDescField**或**SQLSetDescRec**來變更系結的個別詳細資料，而且可以藉由對這些函式進行一系列適當的呼叫，來完全綁定資料行或參數。  
  
 精簡的函數**SQLColAttribute**、 **SQLDescribeCol**、 **SQLDescribeParam**、 **SQLNumParams**和**SQLNumResultCols**會抓取描述項欄位中的值。  
  
 **SQLSetDescRec**和**SQLGetDescRec**是精簡的函式，其中包含一個呼叫、設定或取得會影響資料行或參數資料之資料類型和儲存區的多個描述項欄位。 **SQLSetDescRec**是一種有效的方法，可以在一個步驟中變更資料行或參數資料的系結。  
  
 在某些情況下， **SQLSetStmtAttr**和**SQLGetStmtAttr**會當做精簡的功能來提供。 （請參閱[描述項欄位](../../../odbc/reference/develop-app/descriptor-fields.md)）。

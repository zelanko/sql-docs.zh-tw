---
description: 使用精簡函式
title: 使用簡潔的函式 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b0dcd16c1380c95921d5e4bb58831e2dd939ecf1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482794"
---
# <a name="using-concise-functions"></a>使用精簡函式
某些 ODBC 函數會取得描述項的隱含存取權。 應用程式寫入器可能會發現它們比呼叫 **SQLSetDescField** 或 **SQLGetDescField**更方便。 這些函式稱為 *簡潔* 的函式，因為它們會執行一些函數，包括設定或取得描述項欄位。 有些簡潔的函式可讓應用程式在單一函式呼叫中設定或取出數個相關的描述項欄位。  
  
 您可以呼叫精簡函式，而不需要先取得描述項控制碼以做為引數使用。 這些函數會使用與所呼叫之語句控制碼相關聯的描述項欄位。  
  
 精簡的函式 **SQLBindCol** 和 **SQLBindParameter** 藉由設定對應至其引數的描述項欄位來系結資料行或參數。 每個函式都會執行比單純設定描述項更多的工作。 **SQLBindCol** 和 **SQLBindParameter** 會提供資料行或動態參數之系結的完整規格。 但是，應用程式可以藉由呼叫 **SQLSetDescField** 或 **SQLSetDescRec** 來變更系結的個別詳細資料，而且可以藉由對這些函數進行一連串適當的呼叫，來完全系結資料行或參數。  
  
 精簡的函式 **SQLColAttribute**、 **SQLDescribeCol**、 **SQLDescribeParam**、 **SQLNumParams**和 **SQLNumResultCols** 會取出描述項欄位中的值。  
  
 **SQLSetDescRec** 和 **SQLGetDescRec** 是一種精簡的函式，其中有一個呼叫、設定或取得多重描述項欄位，這些描述項欄位會影響資料行或參數資料的資料類型和儲存。 **SQLSetDescRec** 是一種有效的方法，可讓您在一個步驟中變更資料行或參數資料的系結。  
  
 在某些情況下， **SQLSetStmtAttr**和**SQLGetStmtAttr**可作為簡潔的函式。  (查看 [描述項欄位](../../../odbc/reference/develop-app/descriptor-fields.md)。 ) 

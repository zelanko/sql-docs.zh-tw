---
title: 使用簡明功能 |微軟文件
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
ms.openlocfilehash: 63313e3dfaec8dbcd91f3bb084bbaab46da40c6e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306779"
---
# <a name="using-concise-functions"></a>使用精簡函式
某些 ODBC 函數獲得對描述符的隱式訪問。 應用程式編寫者可能會發現它們比調用**SQLSetDescField**或**SQLGetDescField**更方便。 這些函數稱為*簡潔*函數,因為它們執行許多函數,包括設置或獲取描述符欄位。 某些簡潔的函數允許應用程式在單個函數調用中設置或檢索多個相關的描述符欄位。  
  
 可以調用簡潔函數,而無需首先檢索描述符句柄以用作參數。 這些函數與調用它們的語句句柄關聯的描述符欄位一起工作。  
  
 簡潔函數**SQLBindCol**和**SQLBindParameter**通過設置與其參數對應的描述符欄位來綁定列或參數。 與簡單地設置描述符相比,每個函數執行的任務都更多。 **SQLBindCol**和**SQLBind參數**提供了數據列或動態參數綁定的完整規範。 但是,應用程式可以通過調用**SQLSetDescField**或**SQLSetDescRec**來更改綁定的單個詳細資訊,並且可以通過對這些函數進行一系列適當的調用來完全綁定列或參數。  
  
 簡潔函數**SQLColAttribute**SQLColAttribute、SQLDescribeCol、SQLDescribeParam、SQLNumParams 和**SQLNumResultCols**檢索描述符位**SQLDescribeCol****SQLDescribeParam****SQLNumParams**元的值。  
  
 **SQLSetDescRec**和**SQLGetDescRec**是簡潔的函數,通過一次調用,設置或獲取多個影響列或參數數據的數據類型和存儲的描述符欄位。 **SQLSetDescRec**是一步更改列或參數數據的綁定的有效方法。  
  
 **在某些情況下,SQLSetStmtAttr**和**SQLGetStmtAttr**充當簡潔的功能。 ( 請參考[描述符位元欄位](../../../odbc/reference/develop-app/descriptor-fields.md)。

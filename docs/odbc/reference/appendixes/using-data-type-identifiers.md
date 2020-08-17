---
description: 使用資料類型識別碼
title: 使用資料類型識別碼 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], identifiers
- identifiers [ODBC], data types
ms.assetid: 467e0c0c-a818-4737-8a24-3d8e15c7e162
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 54fe7267ea70dc50b0b40f16b27a1306fea533f2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386274"
---
# <a name="using-data-type-identifiers"></a>使用資料類型識別碼
應用程式會以兩種方式使用資料類型識別碼：若要將其緩衝區描述至驅動程式，以及從驅動程式取出結果集的相關中繼資料，以便判斷要使用哪種類型的 C 緩衝區來儲存資料。 應用程式會呼叫下列函式來執行下列工作：  
  
-   **SQLBindParameter**、 **SQLBindCol**和 **SQLGetData** -描述應用程式緩衝區的 C 資料類型。  
  
-   **SQLBindParameter** -描述動態參數的 SQL 資料類型。  
  
-   **SQLColAttribute** 和 **SQLDescribeCol** -取得結果集資料行的 SQL 資料類型。  
  
-   **SQLDescribeParameter** -用以取出參數的 SQL 資料類型。  
  
-   **SQLColumns**、 **SQLProcedureColumns**和 **SQLSpecialColumns** -用以取出各種架構資訊的 SQL 資料類型  
  
-   **SQLGetTypeInfo** -取得支援的資料類型清單  
  
 資料類型識別碼儲存在描述項的 SQL_DESC_CONCISE_TYPE 欄位中。 描述元函式 **SQLSetDescField** 和 **SQLSetDescRec** 可以搭配適當的類型使用，以執行上述清單中所列的工作。 如需詳細資訊，請參閱 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。

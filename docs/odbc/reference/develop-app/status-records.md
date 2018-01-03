---
title: "狀態記錄 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic records
- status records [ODBC]
- diagnostic records [ODBC]
ms.assetid: 4a987f69-158f-4cc4-a31b-2b7dd8dcbb87
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3ca9f540f779894c06b22ced5e654381d86696ce
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="status-records"></a>狀態記錄
狀態記錄中的欄位包含特定的錯誤或警告驅動程式管理員、 驅動程式或資料來源，包括 SQLSTATE、 自發性錯誤號碼、 診斷訊息、 資料行數目和資料列數目傳回的相關資訊。 此函數會傳回 SQL_ERROR、 SQL_SUCCESS_WITH_INFO、 SQL_NO_DATA、 SQL_NEED_DATA 或 SQL_STILL_EXECUTING 時，才可以建立狀態記錄。 如需狀態記錄中欄位的完整清單，請參閱[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)函式描述。  
  
 此章節包含下列主題。  
  
-   [狀態記錄的順序](../../../odbc/reference/develop-app/sequence-of-status-records.md)  
  
-   [SQLSTATE](../../../odbc/reference/develop-app/sqlstates.md)  
  
-   [診斷訊息](../../../odbc/reference/develop-app/diagnostic-messages.md)

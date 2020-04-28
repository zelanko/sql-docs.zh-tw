---
title: 狀態記錄 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic records
- status records [ODBC]
- diagnostic records [ODBC]
ms.assetid: 4a987f69-158f-4cc4-a31b-2b7dd8dcbb87
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4afef16137404fcdfd3e1d328642f1d314829538
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301369"
---
# <a name="status-records"></a>狀態記錄
狀態記錄中的欄位包含驅動程式管理員、驅動程式或資料來源所傳回之特定錯誤或警告的相關資訊，包括 SQLSTATE、原生錯誤號碼、診斷訊息、資料行編號和資料列編號。 只有在函數傳回 SQL_ERROR、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_NEED_DATA 或 SQL_STILL_EXECUTING 時，才可以建立狀態記錄。 如需狀態記錄中的完整欄位清單，請參閱[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)函數描述。  
  
 此章節包含下列主題。  
  
-   [狀態記錄的順序](../../../odbc/reference/develop-app/sequence-of-status-records.md)  
  
-   [SQLSTATE](../../../odbc/reference/develop-app/sqlstates.md)  
  
-   [診斷訊息](../../../odbc/reference/develop-app/diagnostic-messages.md)

---
title: 狀態記錄 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301369"
---
# <a name="status-records"></a>狀態記錄
狀態記錄中的欄位包含有關驅動程式管理器、驅動程式或資料源返回的特定錯誤或警告的資訊,包括 SQLSTATE、本機錯誤編號、診斷訊息、列號和行號。 僅當函數返回SQL_ERROR、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_NEED_DATA 或SQL_STILL_EXECUTING時,才能創建狀態記錄。 有關狀態記錄中欄位的完整清單,請參閱[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)函數說明。  
  
 此章節包含下列主題。  
  
-   [狀態記錄的順序](../../../odbc/reference/develop-app/sequence-of-status-records.md)  
  
-   [SQLSTATE](../../../odbc/reference/develop-app/sqlstates.md)  
  
-   [診斷訊息](../../../odbc/reference/develop-app/diagnostic-messages.md)

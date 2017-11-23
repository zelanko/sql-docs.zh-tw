---
title: "實作 SQLGetDiagRec 和 SQLGetDiagField |Microsoft 文件"
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
- diagnostic information [ODBC], SqlGetDiagField
- SQLGetDiagField function [ODBC], and SQLGetDiagRec
- SQLGetDiagRec function [ODBC], and SQLGetDiagField
- diagnostic information [ODBC], SqlGetDiagRec
- retrieving diagnostic information [ODBC]
ms.assetid: 11ba1857-b533-4517-8131-a2a8a0154a0a
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d757e4addf483690e491a71d2f7094aa3d9ad116
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="implementing-sqlgetdiagrec-and-sqlgetdiagfield"></a>實作 SQLGetDiagRec 和 SQLGetDiagField
**SQLGetDiagRec**和**SQLGetDiagField**由驅動程式管理員和每個驅動程式。 驅動程式管理員和每個驅動程式負責維護每個環境、 連接、 陳述式，以及描述項處理的診斷記錄，釋放這些記錄，另一個函式呼叫時使用控制代碼或控制代碼會釋出。  
  
 雖然驅動程式管理員和每個驅動程式必須判斷第一個狀態記錄中排名根據[狀態記錄順序](../../../odbc/reference/develop-app/sequence-of-status-records.md)，驅動程式管理員會決定最終的記錄順序。  
  
 **SQLGetDiagRec**和**SQLGetDiagField**不張貼有關本身的診斷記錄。  
  
 此章節包含下列主題。  
  
-   [診斷處理規則](../../../odbc/reference/develop-app/diagnostic-handling-rules.md)  
  
-   [驅動程式管理員的角色](../../../odbc/reference/develop-app/role-of-the-driver-manager.md)  
  
-   [驅動程式的角色](../../../odbc/reference/develop-app/role-of-the-driver.md)

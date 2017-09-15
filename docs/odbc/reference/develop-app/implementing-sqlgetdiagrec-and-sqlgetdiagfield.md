---
title: "實作 SQLGetDiagRec 和 SQLGetDiagField |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- diagnostic information [ODBC], SqlGetDiagField
- SQLGetDiagField function [ODBC], and SQLGetDiagRec
- SQLGetDiagRec function [ODBC], and SQLGetDiagField
- diagnostic information [ODBC], SqlGetDiagRec
- retrieving diagnostic information [ODBC]
ms.assetid: 11ba1857-b533-4517-8131-a2a8a0154a0a
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 463ddfe552c94a9e90ceb2a24f8061674955979d
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="implementing-sqlgetdiagrec-and-sqlgetdiagfield"></a>實作 SQLGetDiagRec 和 SQLGetDiagField
**SQLGetDiagRec**和**SQLGetDiagField**由驅動程式管理員和每個驅動程式。 驅動程式管理員和每個驅動程式負責維護每個環境、 連接、 陳述式，以及描述項處理的診斷記錄，釋放這些記錄，另一個函式呼叫時使用控制代碼或控制代碼會釋出。  
  
 雖然驅動程式管理員和每個驅動程式必須判斷第一個狀態記錄中排名根據[狀態記錄順序](../../../odbc/reference/develop-app/sequence-of-status-records.md)，驅動程式管理員會決定最終的記錄順序。  
  
 **SQLGetDiagRec**和**SQLGetDiagField**不張貼有關本身的診斷記錄。  
  
 此章節包含下列主題。  
  
-   [診斷的處理規則](../../../odbc/reference/develop-app/diagnostic-handling-rules.md)  
  
-   [驅動程式管理員的角色](../../../odbc/reference/develop-app/role-of-the-driver-manager.md)  
  
-   [驅動程式的角色](../../../odbc/reference/develop-app/role-of-the-driver.md)

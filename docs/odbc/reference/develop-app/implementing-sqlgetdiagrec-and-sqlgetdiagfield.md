---
title: 實作 SQLGetDiagRec 和 SQLGetDiagField |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], SqlGetDiagField
- SQLGetDiagField function [ODBC], and SQLGetDiagRec
- SQLGetDiagRec function [ODBC], and SQLGetDiagField
- diagnostic information [ODBC], SqlGetDiagRec
- retrieving diagnostic information [ODBC]
ms.assetid: 11ba1857-b533-4517-8131-a2a8a0154a0a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a4b602d5ff4a94d2888395e6a62f03553fb50f98
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68216371"
---
# <a name="implementing-sqlgetdiagrec-and-sqlgetdiagfield"></a>實作 SQLGetDiagRec 和 SQLGetDiagField
**SQLGetDiagRec**並**SQLGetDiagField**由驅動程式管理員和每個驅動程式。 驅動程式管理員和每個驅動程式維護的每個環境、 連接、 陳述式，以及描述項控制代碼，診斷記錄和另一個函式呼叫會釋放控制代碼或控制代碼時，才可用的記錄。  
  
 雖然每個驅動程式和驅動程式管理員必須判斷第一個的狀態記錄，根據在排名[序號的狀態記錄](../../../odbc/reference/develop-app/sequence-of-status-records.md)，驅動程式管理員會決定最終序列的記錄。  
  
 **SQLGetDiagRec**並**SQLGetDiagField**請勿張貼有關本身的診斷記錄。  
  
 此章節包含下列主題。  
  
-   [診斷處理規則](../../../odbc/reference/develop-app/diagnostic-handling-rules.md)  
  
-   [驅動程式管理員的角色](../../../odbc/reference/develop-app/role-of-the-driver-manager.md)  
  
-   [驅動程式的角色](../../../odbc/reference/develop-app/role-of-the-driver.md)

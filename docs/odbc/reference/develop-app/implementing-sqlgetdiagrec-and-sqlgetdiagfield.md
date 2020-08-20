---
description: 實作 SQLGetDiagRec 和 SQLGetDiagField
title: 執行 SQLGetDiagRec 和 SQLGetDiagField |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 91e43252aea4ebf12dedcb14bb1b7fb34f75df6f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461430"
---
# <a name="implementing-sqlgetdiagrec-and-sqlgetdiagfield"></a>實作 SQLGetDiagRec 和 SQLGetDiagField
**SQLGetDiagRec** 和 **SQLGetDiagField** 是由驅動程式管理員和每個驅動程式所執行。 驅動程式管理員和每個驅動程式都會維護每個環境、連接、語句和描述項控制碼的診斷記錄，而且只有在使用該控制碼呼叫另一個函式或釋放控制碼時，才會釋放這些記錄。  
  
 雖然驅動程式管理員和每個驅動程式都必須根據 [狀態記錄順序](../../../odbc/reference/develop-app/sequence-of-status-records.md)的排名來判斷第一個狀態記錄，驅動程式管理員仍會決定最後的記錄順序。  
  
 **SQLGetDiagRec** 和 **SQLGetDiagField** 不會張貼本身的診斷記錄。  
  
 此章節包含下列主題。  
  
-   [診斷處理規則](../../../odbc/reference/develop-app/diagnostic-handling-rules.md)  
  
-   [驅動程式管理員的角色](../../../odbc/reference/develop-app/role-of-the-driver-manager.md)  
  
-   [驅動程式的角色](../../../odbc/reference/develop-app/role-of-the-driver.md)

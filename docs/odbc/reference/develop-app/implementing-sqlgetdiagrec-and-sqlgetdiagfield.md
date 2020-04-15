---
title: 實現 SQLGetDiagRec 和 SQLGetDiagField |微軟文件
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
ms.openlocfilehash: 4c090af19a9296e46e3036ca23f6c97298bcb1b8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300138"
---
# <a name="implementing-sqlgetdiagrec-and-sqlgetdiagfield"></a>實作 SQLGetDiagRec 和 SQLGetDiagField
**SQLGetDiagRec**和**SQLGetDiagField**由驅動程式管理器和每個驅動程式實現。 驅動程式管理員和每個驅動程式維護每個環境、連接、語句和描述符句柄的診斷記錄,並且僅在使用該句柄調用另一個函數或釋放該句柄時釋放這些記錄。  
  
 儘管驅動程式管理器和每個驅動程式都必須根據[狀態記錄序列](../../../odbc/reference/develop-app/sequence-of-status-records.md)中的排名確定第一個狀態記錄,但驅動程式管理器確定記錄的最終順序。  
  
 **SQLGetDiagRec**和**SQLGetDiagField**不會發布有關自己的診斷記錄。  
  
 此章節包含下列主題。  
  
-   [診斷處理規則](../../../odbc/reference/develop-app/diagnostic-handling-rules.md)  
  
-   [驅動程式管理員的角色](../../../odbc/reference/develop-app/role-of-the-driver-manager.md)  
  
-   [驅動程式的角色](../../../odbc/reference/develop-app/role-of-the-driver.md)

---
title: 狀態記錄序列 |微軟文件
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
ms.assetid: 0e0436cc-230f-44b0-b373-04a57e83ee76
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bb26731a85d1d6313658fe9c24a32167b351d2d9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304169"
---
# <a name="sequence-of-status-records"></a>狀態記錄的順序
如果返回兩個或多個狀態記錄,驅動程式管理器和驅動程式會根據以下規則對它們進行排名。 排名最高的記錄是第一條記錄。 在排名記錄時,不考慮記錄的來源(驅動程式管理器、驅動程式、閘道等)。  
  
-   **錯誤**描述錯誤的狀態記錄的排名最高。 在錯誤記錄中,指示事務失敗或可能事務失敗的記錄超過所有其他記錄。 如果兩個或多個記錄描述相同的錯誤條件,則由開放組 CLI 規範定義的 SQLSTAT(類 03 到 HZ)比 ODBC 定義和驅動程式定義的 SQLSTATEs 高。  
  
-   **設定定義的無資料值**描述驅動程式定義的無資料值(類 02)的狀態記錄具有第二高的排名。  
  
-   **警告**描述警告的狀態記錄(類 01)的排名最低。 如果兩個或多個記錄描述相同的警告條件,則 Open Group CLI 規範定義的警告 SQLSTAT 比 ODBC 定義和驅動程式定義的 SQLSTATA 高。  
  
 如果有兩個或多個排名最高的記錄,則未定義哪個記錄是第一條記錄。 所有其他記錄的順序未定義。 特別是,由於警告可能出現在錯誤之前,因此當函數返回SQL_SUCCESS以外的值時,應用程式應檢查所有狀態記錄。

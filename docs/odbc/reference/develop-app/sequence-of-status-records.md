---
title: 狀態記錄的順序 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304169"
---
# <a name="sequence-of-status-records"></a>狀態記錄的順序
如果傳回兩個或以上的狀態記錄，驅動程式管理員和驅動程式會根據下列規則將它們排序。 具有最高等級的記錄是第一筆記錄。 記錄的來源（驅動程式管理員、驅動程式、閘道等）不會在排名記錄時考慮。  
  
-   **錯誤**描述錯誤的狀態記錄具有最高等級。 在錯誤記錄中，表示交易失敗或可能發生交易失敗的記錄會 outrank 所有其他記錄。 如果有兩個以上的記錄描述相同的錯誤狀況，則 SQLSTATEs 由 Open Group CLI 規格（類別03到 HZ）定義，outrank ODBC 定義和驅動程式定義的 SQLSTATEs。  
  
-   **執行-未定義任何資料值**描述驅動程式定義的無資料值（類別02）的狀態記錄具有第二個最高等級。  
  
-   **警告**描述警告的狀態記錄（類別01）具有最低的排名。 如果有兩個或多筆記錄描述相同的警告條件，則「開啟群組 CLI」規格所定義的警告 SQLSTATEs 會 outrank ODBC 定義和驅動程式定義的 SQLSTATEs。  
  
 如果有兩個以上的記錄具有最高等級，則會未定義哪一筆記錄是第一筆記錄。 所有其他記錄的順序都未定義。 特別是，因為警告可能會在錯誤發生之前出現，所以應用程式應該在函式傳回 SQL_SUCCESS 以外的值時，檢查所有狀態記錄。

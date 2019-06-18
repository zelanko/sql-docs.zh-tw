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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 17a88095611a5f551708f3950359063317368757
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62465914"
---
# <a name="sequence-of-status-records"></a>狀態記錄的順序
如果傳回兩個或多個狀態記錄，在驅動程式管理員和驅動程式進行排名，根據下列規則。 具有最高順位的記錄是第一筆記錄。 資料錄 （驅動程式管理員、 驅動程式、 閘道和等等） 的來源不是當排名的記錄。  
  
-   **錯誤**描述錯誤的狀態記錄都有最高的等級。 在錯誤記錄，表示交易失敗或可能的交易失敗的記錄會 outrank 其他所有記錄。 如果兩個或多筆記錄會描述相同的錯誤狀況，開啟群組 CLI 規格 （透過 HZ 類別 03） 所定義的 Sqlstate outrank ODBC 定義及驅動程式定義的 Sqlstate。  
  
-   **實作定義沒有資料值**描述驅動程式定義沒有資料值 （類別 02） 的狀態記錄的第二個最高的等級。  
  
-   **警告**描述警告 （類別 01） 的狀態記錄具有最低順位。 如果兩個或多筆記錄會描述相同的警告條件，警告開啟群組 CLI 規格所定義的 Sqlstate outrank ODBC 定義及驅動程式定義的 Sqlstate。  
  
 如果有兩個或多個記錄，最高陣序規範，並未定義哪一筆記錄是第一筆記錄。 未定義的所有其他的記錄順序。 特別是之前的錯誤,，可能會出現警告，因為應用程式時應檢查狀態的所有記錄的函式會傳回 SQL_SUCCESS 以外的值。

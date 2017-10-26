---
title: "狀態記錄的序列 |Microsoft 文件"
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
- diagnostic information [ODBC], diagnostic records
- status records [ODBC]
- diagnostic records [ODBC]
ms.assetid: 0e0436cc-230f-44b0-b373-04a57e83ee76
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b0e11fdd0d5d560cfcacd034745f7ed32cf8fca8
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sequence-of-status-records"></a>狀態記錄的序列
如果傳回兩個或多個狀態記錄，在驅動程式管理員和驅動程式進行排名，根據下列規則。 具有最高等級的記錄是第一筆記錄。 資料錄 （驅動程式管理員、 驅動程式、 閘道和等等） 的來源不會被視為時排序記錄。  
  
-   **錯誤**描述錯誤的狀態記錄擁有最高的等級。 錯誤的記錄，表示交易失敗或可能的交易失敗的記錄 outrank 所有其他的記錄。 如果兩個或多個記錄描述相同的錯誤狀況，請開啟群組 CLI 規格 （透過 HZ 類別 03） 所定義的 Sqlstate outrank ODBC 定義及驅動程式定義的 Sqlstate。  
  
-   **實作定義沒有資料值**描述驅動程式定義沒有資料值 （類別 02） 的狀態記錄都有第二個最高的等級。  
  
-   **警告**描述警告 （類別 01） 的狀態記錄具有最低順位。 如果兩個或多個記錄描述警告 Sqlstate 開啟群組 CLI 規格所定義的相同警告條件 outrank ODBC 定義及驅動程式定義的 Sqlstate。  
  
 如果沒有具有最高等級的兩個或多個記錄，它是未定義的記錄是第一筆記錄。 未定義的所有其他的記錄順序。 特別是之前的錯誤,，可能會出現警告，因為應用程式時應檢查所有的狀態記錄函式會傳回 SQL_SUCCESS 以外的值。


---
title: 並行控制 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], concurrency control
- concurrency control [ODBC]
ms.assetid: 75e4adb3-3d43-49c5-8c5e-8df96310d912
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8afba3b3b8c8fee1307473c790186d509b37d982
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294848"
---
# <a name="concurrency-control"></a>並行控制
*併發*性是兩個事務同時使用相同的數據的能力,隨著事務隔離的增加,併發性通常會減少。 這是因為事務隔離通常是通過鎖定行實現的,並且隨著鎖定的行數增加,可以完成較少的事務,而不會至少被鎖定的行臨時阻止。 雖然減少併發性通常被認為是對維護資料庫完整性所需的更高事務隔離級別的權衡,但在具有使用游標的高讀/寫活動的互動式應用程式中,它可能成為一個問題。  
  
 例如,假設應用程式執行 SQL 語句 **「從訂單\*中選擇**」。 它調用**SQLFetchScroll**滾動結果集,並允許使用者更新、刪除或插入訂單。 使用者更新、刪除或插入訂單后,應用程式將提交事務。  
  
 如果隔離級別是可重複讀取,則事務可能會(取決於實現方式)鎖定**SQLFetchScroll**返回的每一行。 如果隔離級別是可序列化的,則事務可能會鎖定整個訂單表。 在這兩種情況下,事務僅在提交或回滾時釋放其鎖。 因此,如果用戶花費大量時間閱讀訂單,而更新、刪除或插入訂單的時間很少,則事務可以輕鬆地鎖定大量行,從而使其他使用者無法訪問這些行。  
  
 這是一個問題,即使游標是唯讀的,並且應用程式允許使用者唯讀取現有訂單。 在這種情況下,應用程式在調用**SQLCloseCursor(** 在自動提交模式下)或**SQLEndTran(** 在手動提交模式下)時提交事務並釋放鎖。  
  
 此章節包含下列主題。  
  
-   [並行類型](../../../odbc/reference/develop-app/concurrency-types.md)  
  
-   [開放式並行存取](../../../odbc/reference/develop-app/optimistic-concurrency.md)

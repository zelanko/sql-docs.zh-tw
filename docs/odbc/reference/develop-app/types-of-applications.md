---
title: "類型的應用程式 |Microsoft 文件"
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
- upgrading applications [ODBC], application types
- backward compatibility [ODBC], application and driver compatibility
- compatibility [ODBC], application and driver compatibility
- application upgrades [ODBC], application types
- application compatibility issues [ODBC]
ms.assetid: d346a64e-a32c-4153-a40f-5b53c2f57ef2
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3cca547e091ffdd601550b5cfb4ddb6b078f0900
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="types-of-applications"></a>類型的應用程式
ODBC 應用程式分類如下：  
  
-   **純的 ODBC 2。**  
     ***x*應用程式**的 32 位元應用程式的：  
  
    -   呼叫 ODBC 2。*x*函式 (包括 ODBC 1.0 函式**SQLSetParam**)。 這些包括 ODBC 1。*x*已移植至 32 位元的應用程式。  
  
    -   必須要有 ODBC 2。*x*有行為變更的功能的行為。 (請參閱[的行為變更](../../../odbc/reference/develop-app/behavioral-changes.md)如需詳細資訊。)  
  
    -   具有未重新編譯 ODBC 3.5 標頭。  
  
-   **純的 ODBC 2。**  
     ***x*重新編譯應用程式**單純的 ODBC 2。*x*已使用 ODBC 3.5 標頭檔中，重新編譯的應用程式藉由設定 ODBCVER = 0x0250。  
  
-   **純的 ODBC 2。**  
     ***x* Unicode 應用程式**單純的 ODBC 2。*x*重新編譯應用程式與 Unicode 相容，並且使用 SQL_WCHAR 資料類型。  
  
-   **純的 Open Group 和 ISO**–**相容的 ODBC 應用程式**的 32 位元應用程式的：  
  
    -   呼叫 Open Group 或 CLI ISO 標準中定義的函式。 （這些函式可能會包含已被取代的 3.0 函式）。  
  
    -   不使用 Unicode 資料類型。  
  
    -   必須要有 ODBC 3.0 行為有行為變更的功能。  
  
-   **純的 ODBC 3.0 應用程式**的 32 位元應用程式的：  
  
    -   會編譯包含 3.0 版的標頭。  
  
    -   呼叫任何 ODBC 3.0 函數時，可能會包含這些已被取代。  
  
    -   必須要有 ODBC 3.0 行為有行為變更的功能。  
  
-   **純的 ODBC 3.5 應用程式**32 或 64 位元應用程式的：  
  
    -   可能會使用 Unicode 資料類型。  
  
    -   呼叫任何 ODBC 3.5 函數時，可能會包含這些已被取代。  
  
    -   必須要有 ODBC 3.5 行為有行為變更的功能。  
  
-   **純 ODBC 3.8 （或更新版本） 應用程式**的 32 位元或 64 位元應用程式的：  
  
    -   可能會使用 Unicode 資料類型。  
  
    -   呼叫任何 ODBC 3.8 函數時，可能會包含這些已被取代。  
  
    -   必須要有 ODBC 3.8 行為有行為變更的功能。  
  
-   **取代應用程式**32 或 64 位元應用程式的：  
  
    -   實作的重複功能的新行為。  
  
    -   只有在條件式程式碼內 ODBC 較新版本中使用的任何新功能。  
  
    -   已經將本身是較早版本的 ODBC 應用程式註冊或已限制條件的程式碼來處理的行為變更。

---
title: 類型的應用程式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- upgrading applications [ODBC], application types
- backward compatibility [ODBC], application and driver compatibility
- compatibility [ODBC], application and driver compatibility
- application upgrades [ODBC], application types
- application compatibility issues [ODBC]
ms.assetid: d346a64e-a32c-4153-a40f-5b53c2f57ef2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 50e3e733a4ddd4855da2ea7722407e5f061eee47
ms.sourcegitcommit: bfa10c54e871700de285d7f819095d51ef70d997
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/14/2019
ms.locfileid: "54255793"
---
# <a name="types-of-applications"></a>應用程式的類型
ODBC 應用程式分類如下：  
  
-   **純的 ODBC 2。**  
     **_x_應用程式**的 32 位元應用程式的：  
  
    -   呼叫 ODBC 2。*x*函式 (包括 ODBC 1.0 函式**SQLSetParam**)。 這些包括 ODBC 1。*x*已移植至 32 位元的應用程式。  
  
    -   必須要有 ODBC 2。*x*有行為變更的功能的行為。 (請參閱[的行為變更](../../../odbc/reference/develop-app/behavioral-changes.md)如需詳細資訊。)  
  
    -   具有未重新編譯 ODBC 3.5 標頭。  
  
-   **純的 ODBC 2。**  
     **_x_重新編譯應用程式**純粹的 ODBC 2。*x*已使用 ODBC 3.5 標頭檔中，重新編譯的應用程式藉由設定 ODBCVER = 0x0250。  
  
-   **純的 ODBC 2。**  
     **_x_ Unicode 應用程式**純粹的 ODBC 2。*x*重新編譯應用程式與 Unicode 相容，並且使用 SQL_WCHAR 資料類型。  
  
-   **純的 Open Group 和 ISO**-**相容的 ODBC 應用程式**的 32 位元應用程式的：  
  
    -   呼叫 Open Group 或 ISO CLI 標準中定義的函式。 （這些函式可能包含已被取代的 3.0 函式）。  
  
    -   不使用 Unicode 資料類型。  
  
    -   預期有的行為變更的功能的 ODBC 3.0 行為。  
  
-   **純的 ODBC 3.0 應用程式**的 32 位元應用程式的：  
  
    -   會編譯使用 3.0 版的標頭。  
  
    -   呼叫任何 ODBC 3.0 函數時，可能包括已被取代。  
  
    -   預期有的行為變更的功能的 ODBC 3.0 行為。  
  
-   **純的 ODBC 3.5 應用程式**32 或 64 位元應用程式的：  
  
    -   可能會使用 Unicode 資料類型。  
  
    -   呼叫任何 ODBC 3.5 函數時，可能包括已被取代。  
  
    -   預期有的行為變更的功能的 ODBC 3.5 行為。  
  
-   **純 ODBC 3.8 （或更新版本） 應用程式**的 32 位元或 64 位元應用程式的：  
  
    -   可能會使用 Unicode 資料類型。  
  
    -   呼叫任何 ODBC 3.8 函數時，可能包括已被取代。  
  
    -   需要 ODBC 3.8 行為有行為變更的功能。  
  
-   **取代應用程式**32 或 64 位元應用程式的：  
  
    -   重複的功能會實作新行為。  
  
    -   使用 ODBC 較新版本，只有在條件式的程式碼中的任何新功能。  
  
    -   已經將本身是較早版本的 ODBC 應用程式註冊或已限制條件的程式碼來處理行為的變更。

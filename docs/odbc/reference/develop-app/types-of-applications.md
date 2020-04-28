---
title: 應用程式類型 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f14326c9cec1eb89e431154c91b680e4688fcdfa
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305529"
---
# <a name="types-of-applications"></a>應用程式的類型
ODBC 應用程式可以分類如下：  
  
-   **純粹的 ODBC 2。**  
     ** _x_應用程式**A 32 位應用程式：  
  
    -   只呼叫 ODBC 2。*x*函數（包括 ODBC 1.0 函數**SQLSetParam**）。 這些包括 ODBC 1。已移植到32位的*x*應用程式。  
  
    -   預期 ODBC 2。具有行為變更之功能的*x*行為。 （如需詳細資訊，請參閱[行為變更](../../../odbc/reference/develop-app/behavioral-changes.md)）。  
  
    -   尚未使用 ODBC 3.5 標頭進行重新編譯。  
  
-   **純粹的 ODBC 2。**  
     **_x_重新編譯的應用程式**A 單純的 ODBC 2。已使用 ODBC 3.5 標頭檔重新編譯的*x*應用程式，方法是設定 ODBCVER = 0x0250。  
  
-   **純粹的 ODBC 2。**  
     **_x_ Unicode 應用程式**：純 ODBC 2。已*重新編譯符合*Unicode 標準的應用程式，並使用 SQL_WCHAR 的資料類型。  
  
-   **純開放式群組和符合 ISO**-**規範的 ODBC 應用程式**A 32 位應用程式：  
  
    -   呼叫開放式群組或 ISO CLI 標準中定義的函數。 （這些函數可能包含已被取代的3.0 函式）。  
  
    -   不使用 Unicode 資料類型。  
  
    -   預期具有行為變更之功能的 ODBC 3.0 行為。  
  
-   **純 ODBC 3.0 應用程式**32位應用程式，其：  
  
    -   會使用3.0 標頭進行編譯。  
  
    -   呼叫任何 ODBC 3.0 函數，可能包含已被取代的函式。  
  
    -   預期具有行為變更之功能的 ODBC 3.0 行為。  
  
-   **純 ODBC 3.5 應用程式**32或64位應用程式，其：  
  
    -   可能會使用 Unicode 資料類型。  
  
    -   呼叫任何 ODBC 3.5 函數，可能包含已被取代的函式。  
  
    -   預期具有行為變更之功能的 ODBC 3.5 行為。  
  
-   **單純的 ODBC 3.8 （或更新版本）應用程式**32位或64位應用程式，其：  
  
    -   可能會使用 Unicode 資料類型。  
  
    -   呼叫任何 ODBC 3.8 函數，可能包含已被取代的函式。  
  
    -   預期具有行為變更之功能的 ODBC 3.8 行為。  
  
-   **已取代應用程式**32或64位應用程式，其：  
  
    -   為重複的功能實行新的行為。  
  
    -   只會在條件式程式碼內使用較新版本的 ODBC 中的任何新功能。  
  
    -   具有有限的條件式程式碼來處理行為變更，或已將其本身註冊為舊版的 ODBC 應用程式。

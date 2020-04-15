---
title: 應用程式類型 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305529"
---
# <a name="types-of-applications"></a>應用程式的類型
ODBC 應用程式可分類如下:  
  
-   **純 ODBC 2.**  
     ** _x_應用程式**A 32 位元應用程式, :  
  
    -   僅調用 ODBC 2。*x*函數(包括 ODBC 1.0 函數**SQLSetParam**)。 其中包括ODBC 1。*已*移植到 32 位的 x 應用程式。  
  
    -   預期 ODBC 2.*具有*行為更改的功能的 x 行為。 (有關詳細資訊,請參閱[行為更改](../../../odbc/reference/develop-app/behavioral-changes.md)。  
  
    -   尚未使用 ODBC 3.5 標頭重新編譯。  
  
-   **純 ODBC 2.**  
     **_x_重新編譯應用程式**純 ODBC 2。*x*使用 ODBC 3.5 標頭檔重新編譯的應用程式,通過設定 ODBCVER=0x0250。  
  
-   **純 ODBC 2.**  
     **_x_ Unicode 應用程式**純 ODBC 2。*x*重新編譯的應用程式符合 Unicode,並使用SQL_WCHAR數據類型。  
  
-   **純開放群組和符合 ISO**-**標準的 ODBC 應用程式**A 32 位元應用程式,它:  
  
    -   在開放組或 ISO CLI 標準中定義的調用函數。 (這些函數可能包括棄用的 3.0 函數。  
  
    -   不使用 Unicode 數據類型。  
  
    -   對於行為更改的要素,預期 ODBC 3.0 行為。  
  
-   **純 ODBC 3.0 應用**32 位元應用程式,它:  
  
    -   使用 3.0 標頭編譯。  
  
    -   調用任何 ODBC 3.0 函數,可能包括已棄用的功能。  
  
    -   對於行為更改的要素,預期 ODBC 3.0 行為。  
  
-   **純 ODBC 3.5 應用**32 位元或 64 位元應用程式,它:  
  
    -   可以使用 Unicode 資料類型。  
  
    -   調用任何 ODBC 3.5 函數,可能包括已棄用的功能。  
  
    -   對於行為更改的要素,預期 ODBC 3.5 行為。  
  
-   **純 ODBC 3.8(或更高版本)應用**32 位元或 64 位元應用程式,它:  
  
    -   可以使用 Unicode 資料類型。  
  
    -   調用任何 ODBC 3.8 函數,可能包括已棄用的功能。  
  
    -   對於行為更改的要素,預期 ODBC 3.8 行為。  
  
-   **取代應用程式**32 位元或 64 位元應用程式,它:  
  
    -   為重複的功能實現新行為。  
  
    -   僅在條件代碼中使用更高版本的 ODBC 中的任何新功能。  
  
    -   具有用於處理行為更改的條件代碼有限,或已註冊為 ODBC 應用程式的早期版本。

---
description: 應用程式的類型
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
ms.openlocfilehash: 54056a6111924fb584ac35a65d6f74e8dab1ba6c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465548"
---
# <a name="types-of-applications"></a>應用程式的類型
ODBC 應用程式可以分類如下：  
  
-   **純 ODBC 2。**  
     ** _x_應用程式**A 32 位應用程式：  
  
    -   只呼叫 ODBC 2。*x* 函數 (包括 ODBC 1.0 函式 **SQLSetParam**) 。 這些包括 ODBC 1。已移植到32位的*x* 應用程式。  
  
    -   預期 ODBC 2。具有行為變更之功能的*x* 行為。  (如需詳細資訊，請參閱 [行為變更](../../../odbc/reference/develop-app/behavioral-changes.md) 。 )   
  
    -   尚未使用 ODBC 3.5 標頭重新編譯。  
  
-   **純 ODBC 2。**  
     **_x_ 重新編譯的應用程式** 是純 ODBC 2。已使用 ODBC 3.5 標頭檔重新編譯的*x* 應用程式，方法是設定 ODBCVER = 0x0250。  
  
-   **純 ODBC 2。**  
     **_x_ Unicode 應用程式** ：純 ODBC 2。符合 Unicode 標準並使用 SQL_WCHAR 資料類型的*x* 重新編譯應用程式。  
  
-   **純開放式群組和 ISO** -**符合規範的 ODBC 應用程式**32位應用程式：  
  
    -   呼叫開放式群組或 ISO CLI 標準中定義的函式。  (這些函式可能包含已淘汰的3.0 函數。 )   
  
    -   不使用 Unicode 資料類型。  
  
    -   預期具有行為變更之功能的 ODBC 3.0 行為。  
  
-   **純 ODBC 3.0 應用程式** 32位應用程式：  
  
    -   使用3.0 標頭進行編譯。  
  
    -   呼叫任何 ODBC 3.0 函式，可能包含已被取代的函數。  
  
    -   預期具有行為變更之功能的 ODBC 3.0 行為。  
  
-   **純 ODBC 3.5 應用程式** 32或64位應用程式，其：  
  
    -   可以使用 Unicode 資料類型。  
  
    -   呼叫任何 ODBC 3.5 函式，可能包含已被取代的函數。  
  
    -   預期具有行為變更之功能的 ODBC 3.5 行為。  
  
-   **純 ODBC 3.8 (或更新版本) 應用程式** 32位或64位應用程式，其：  
  
    -   可以使用 Unicode 資料類型。  
  
    -   呼叫任何 ODBC 3.8 函式，可能包含已被取代的函數。  
  
    -   預期具有行為變更之功能的 ODBC 3.8 行為。  
  
-   **取代的應用程式** 32或64位應用程式，其：  
  
    -   為重複的功能實行新的行為。  
  
    -   只會在條件式程式碼中使用較新版本的 ODBC 中的任何新功能。  
  
    -   具有限制行為變更或已註冊本身為舊版 ODBC 應用程式的條件式程式碼。

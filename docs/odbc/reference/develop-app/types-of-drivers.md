---
title: 類型的驅動程式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver compatibility issues [ODBC]
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], application and driver compatibility
- compatibility [ODBC], application and driver compatibility
ms.assetid: 864c53c1-b68a-48b6-b6bc-5ecb520bb9dc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ea99ec6a5b0a76ce0647e3681a4cf919d3f086b6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68087768"
---
# <a name="types-of-drivers"></a>驅動程式的類型
ODBC 驅動程式可以分類如下：  
  
-   **32 位元 ODBC 2。**  
     **_x_驅動程式**的 32 位元驅動程式會：  
  
    -   匯出只 ODBC *2.x*函式。  
  
    -   顯示 ODBC *2.x*行為的行為變更。  
  
-   **ISO 和開啟群組相容的驅動程式**的 32 位元驅動程式會：  
  
    -   開啟 群組或 ISO CLI 文件中所述的所有函式會將匯出。 這會在 ODBC 中包含一些已被取代的函式。  
  
    -   表現的行為變更的 ODBC 3.0 行為。  
  
    -   不一定會透過 ODBC 3.0 驅動程式管理員。  
  
-   **ODBC 3.0 驅動程式**的 32 位元驅動程式會：  
  
    -   減去 ODBC 3.0 中的匯出唯一函式已取代函式。  
  
    -   能夠發生 ODBC *2.x*行為上的變更，而言，ODBC 3.0 行為根據 SQL_ATTR_APP_ODBC_VERSION 環境屬性。  
  
-   **ODBC 3.5 （含） 以後 ANSI 的驅動程式**的 32 位元驅動程式會：  
  
    -   減去 ODBC 3.5 中的匯出唯一函式已取代函式。  
  
    -   能夠發生 ODBC *2.x*行為或 ODBC 3.0 行為上的變更，而言，ODBC 3.5 行為根據 SQL_ATTR_APP_ODBC_VERSION 環境屬性。  
  
-   **ODBC 3.5 （含） 以後 Unicode 驅動程式**的 32 位元驅動程式會：  
  
    -   支援 ODBC 3.5 ANSI 驅動程式的所有功能。  
  
    -   將匯出所有 ODBC 字串 Api 的 Unicode 的版本。  
  
    -   可以儲存及處理資料來源上的 Unicode 資料。  
  
> [!NOTE]  
>  16 位元 ODBC 驅動程式無法直接與 ODBC *3.x*驅動程式管理員。 但是，它可能是 16 位元驅動程式，才能使用 2.0 的 ODBC 驅動程式管理員，這後續 thunk 達*3.x*驅動程式管理員。

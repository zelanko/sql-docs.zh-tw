---
title: 驅動程式的類型 |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68087768"
---
# <a name="types-of-drivers"></a>驅動程式的類型
ODBC 驅動程式可以分類如下：  
  
-   **32位 ODBC 2。**  
     ** _x_驅動程式**A 32 位驅動程式：  
  
    -   只*匯出 ODBC 2.x*函數。  
  
    -   展示行為*變更的 ODBC 2.x*行為。  
  
-   **ISO 和開放式群組相容的驅動程式**32位驅動程式：  
  
    -   匯出開啟的群組或 ISO CLI 檔中記載的所有函式。 這會包含一些在 ODBC 中被取代的函式。  
  
    -   展示行為變更的 ODBC 3.0 行為。  
  
    -   不一定會經過 ODBC 3.0 驅動程式管理員。  
  
-   **ODBC 3.0 驅動程式**32位驅動程式：  
  
    -   只匯出 ODBC 3.0 中的函式減去已被取代的函式。  
  
    -   可以根據 SQL_ATTR_APP_ODBC_VERSION 環境屬性，來提供 ODBC *2.x 行為或 odbc 3.0*行為（關於行為變更）。  
  
-   **ODBC 3.5 （或更新版本） ANSI 驅動程式**32位驅動程式：  
  
    -   只匯出 ODBC 3.5 中的函式減去已被取代的函式。  
  
    -   可以根據 SQL_ATTR_APP_ODBC_VERSION 環境屬性，來提供 ODBC *2.x 行為或 odbc 3.0 行為，* 或 odbc 3.5 行為（關於行為變更）。  
  
-   **ODBC 3.5 （或更新版本） Unicode 驅動程式**32位驅動程式：  
  
    -   支援 ODBC 3.5 ANSI 驅動程式的所有功能。  
  
    -   匯出所有 ODBC 字串 Api 的 Unicode 版本。  
  
    -   可以在資料來源上儲存和處理 Unicode 資料。  
  
> [!NOTE]  
>  16位 ODBC 驅動程式將無法直接*與 ODBC 3.X*驅動程式管理員搭配使用。 不過，16位驅動程式可能會與 2.0 ODBC 驅動程式管理員搭配使用，而這也是一種可轉型為*3.X 驅動程式管理員的方式*。

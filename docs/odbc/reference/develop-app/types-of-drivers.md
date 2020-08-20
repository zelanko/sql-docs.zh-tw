---
description: 驅動程式的類型
title: 驅動程式類型 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4ae3ab2b0172e97a221b446107ccbf4b6ae4eb7b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476292"
---
# <a name="types-of-drivers"></a>驅動程式的類型
ODBC 驅動程式可以分類如下：  
  
-   **32位 ODBC 2。**  
     ** _x_驅動程式**A 32 位驅動程式：  
  
    -   只 *匯出 ODBC 2.x* 函數。  
  
    -   展示 ODBC *2.x 行為的行為變更* 。  
  
-   **ISO 和開放式群組相容驅動程式** 32位驅動程式：  
  
    -   匯出開啟的群組或 ISO CLI 檔中記載的所有功能。 這會包含一些在 ODBC 中被取代的函數。  
  
    -   展示行為變更的 ODBC 3.0 行為。  
  
    -   不一定會經過 ODBC 3.0 驅動程式管理員。  
  
-   **ODBC 3.0 驅動程式** 32位驅動程式：  
  
    -   只匯出 ODBC 3.0 中的函式，減去已被取代的函式。  
  
    -   可以根據 SQL_ATTR_APP_ODBC_VERSION 環境屬性，針對行為變更，來 *提供 odbc 2.x 行為或 odbc 3.0* 行為。  
  
-   **ODBC 3.5 (或更新版本) ANSI 驅動程式** 32位驅動程式：  
  
    -   只匯出 ODBC 3.5 中的函式，減去已被取代的函式。  
  
    -   根據 SQL_ATTR_APP_ODBC_VERSION 環境屬性，能夠根據行為變更，來提供 ODBC *2.x 行為或* odbc 3.0 行為或 odbc 3.5 行為。  
  
-   **ODBC 3.5 (或更新版本) Unicode 驅動程式** 32位驅動程式：  
  
    -   支援 ODBC 3.5 ANSI 驅動程式的所有功能。  
  
    -   匯出所有 ODBC 字串 Api 的 Unicode 版本。  
  
    -   可以儲存和處理資料來源上的 Unicode 資料。  
  
> [!NOTE]  
>  16位的 ODBC 驅動程式不會直接 *使用 odbc 3.X* 驅動程式管理員。 不過，16位驅動程式有可能與 2.0 ODBC 驅動程式管理員搭配使用，而後者接著會成為*3.X 驅動程式管理員。*

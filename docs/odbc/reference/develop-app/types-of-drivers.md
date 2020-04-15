---
title: 驅動程式型態 :微軟文件
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
ms.openlocfilehash: de6d8e1473f127d28c69969e0fc298afd69d3023
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304869"
---
# <a name="types-of-drivers"></a>驅動程式的類型
ODBC 驅動程式可以分類如下:  
  
-   **32 位元 ODBC 2。**  
     ** _x_驅動程式**32 位元驅動程式, :  
  
    -   僅匯出 ODBC *2.x*功能。  
  
    -   展示 ODBC *2.x*行為變化的行為。  
  
-   **ISO 與開啟群組相容驅動程式**32 位驅動程式,  
  
    -   匯出在開放組或 ISO CLI 文件中記錄的所有功能。 這將包括一些在 ODBC 中棄用的功能。  
  
    -   展示 ODBC 3.0 行為更改的行為。  
  
    -   不一定透過 ODBC 3.0 驅動程式管理員。  
  
-   **ODBC 3.0 驅動程式**32 位驅動程式,  
  
    -   僅匯出 ODBC 3.0 減去棄用函數中的函數。  
  
    -   能夠根據SQL_ATTR_APP_ODBC_VERSION環境屬性,在行為變化方面展示 ODBC *2.x*行為或 ODBC 3.0 行為。  
  
-   **ODBC 3.5(或更高版本)ANSI 驅動程式**32 位驅動程式,  
  
    -   僅匯出 ODBC 3.5 減去棄用函數中的函數。  
  
    -   能夠根據SQL_ATTR_APP_ODBC_VERSION環境屬性,展示ODBC *2.x*行為或ODBC 3.0行為,或ODBC 3.5行為行為。  
  
-   **ODBC 3.5(或更高版本)統一代碼驅動程式**32 位驅動程式,  
  
    -   支援 ODBC 3.5 ANSI 驅動程式的所有功能。  
  
    -   匯出所有 ODBC 字串 API 的 Unicode 版本。  
  
    -   可以在數據源上存儲和處理 Unicode 資料。  
  
> [!NOTE]  
>  16 位元 ODBC 驅動程式不會直接與 ODBC *3.x*驅動程式管理員配合使用。 但是,16 位元驅動程式可以使用 2.0 ODBC 驅動程式管理器,該管理器隨後會連接到*3.x*驅動程式管理器。

---
title: 類型的驅動程式 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- driver compatibility issues [ODBC]
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], application and driver compatibility
- compatibility [ODBC], application and driver compatibility
ms.assetid: 864c53c1-b68a-48b6-b6bc-5ecb520bb9dc
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e75e5827becd5457d0e310ca5ec0cc2a13259be5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32914683"
---
# <a name="types-of-drivers"></a>類型的驅動程式
ODBC 驅動程式可分類如下：  
  
-   **32 位元 ODBC 2。**  
     ***x*驅動程式**的 32 位元驅動程式的：  
  
    -   匯出只 ODBC 2 *.x*函式。  
  
    -   表現 ODBC 2。*x*行為的行為變更。  
  
-   **ISO 和開啟群組相容的驅動程式**的 32 位元驅動程式的：  
  
    -   開啟 群組或 ISO CLI 文件中所述的所有函式會將匯出。 這會將包含部分已被取代的函式 ODBC。  
  
    -   表現的行為變更的 ODBC 3.0 行為。  
  
    -   不一定討論透過 ODBC 3.0 驅動程式管理員。  
  
-   **ODBC 3.0 驅動程式**的 32 位元驅動程式的：  
  
    -   減 ODBC 3.0 中的匯出唯一函式已被取代的函式。  
  
    -   能夠呈現 ODBC 2。*x*行為或行為的變更，ODBC 3.0 行為根據 SQL_ATTR_APP_ODBC_VERSION 環境屬性。  
  
-   **ODBC 3.5 （含） 以後 ANSI 驅動程式**的 32 位元驅動程式的：  
  
    -   減 ODBC 3.5 中的匯出唯一函式已被取代的函式。  
  
    -   能夠呈現 ODBC 2。*x*行為或 ODBC 3.0 行為或行為的變更，ODBC 3.5 行為根據 SQL_ATTR_APP_ODBC_VERSION 環境屬性。  
  
-   **ODBC 3.5 （含） 以後 Unicode 的驅動程式**的 32 位元驅動程式的：  
  
    -   支援 ODBC 3.5 ANSI 驅動程式的所有功能。  
  
    -   匯出所有 ODBC 字串應用程式開發介面的 Unicode 版本。  
  
    -   可以儲存及處理資料來源上的 Unicode 資料。  
  
> [!NOTE]  
>  16 位元 ODBC 驅動程式直接與 ODBC 3，將無法運作。*x*驅動程式管理員。 不過，它可能會使用 2.0 的 ODBC 驅動程式管理員，其隨後 thunk 最多 3 個 16 位元驅動程式。*x*驅動程式管理員。

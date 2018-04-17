---
title: 判斷資料指標的功能 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], capabilities
- cursors [ODBC], scrollable
ms.assetid: 35be486c-8f2d-4cec-beb8-df14151abfef
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7c97f09c2f0768b7c0c031ed1176761d5fde06ee
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="determining-cursor-capabilities"></a>判斷資料指標的功能
中的下列四個選項**SQLGetInfo**說明支援的資料指標類型和功能為何：  
  
-   SQL_CURSOR_SENSITIVITY。 指出資料指標是否為另一個資料指標所做的變更影響。  
  
-   SQL_SCROLL_OPTIONS。 列出支援的資料指標類型 （順向、 靜態、 索引鍵集驅動、 動態的或混合）。 所有資料來源必須都支援順向資料指標。  
  
-   SQL_DYNAMIC_CURSOR_ATTRIBUTES1、 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1 SQL_KEYSET_CURSOR_ATTRIBUTES1 或 SQL_STATIC_CURSOR_ATTRIBUTES1 （取決於資料指標的類型）。 列出可捲動資料指標所支援的 fetch 類型。 傳回值中的位元會對應到以提取**SQLFetchScroll**。  
  
-   SQL_KEYSET_CURSOR_ATTRIBUTES2 或 SQL_STATIC_CURSOR_ATTRIBUTES2 （取決於資料指標的類型）。 列出靜態和索引鍵集驅動資料指標可以偵測到自己的更新、 刪除和插入。  
  
 應用程式可以判斷在執行階段資料指標的功能藉由呼叫**SQLGetInfo**與這些選項。 這通常是由泛型應用程式。 資料指標的功能也可以判斷在應用程式開發和使用硬式編碼至應用程式。 這通常是垂直和自訂應用程式，但也可藉由使用用戶端資料指標實作，例如 ODBC 資料指標程式庫的泛型應用程式。

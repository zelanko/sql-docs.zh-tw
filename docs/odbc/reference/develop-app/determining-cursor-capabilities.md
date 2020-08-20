---
description: 判斷資料指標的功能
title: 判斷資料指標功能 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], capabilities
- cursors [ODBC], scrollable
ms.assetid: 35be486c-8f2d-4cec-beb8-df14151abfef
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3390f83a30f6f462148d477ec018d1209ee6e098
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465820"
---
# <a name="determining-cursor-capabilities"></a>判斷資料指標的功能
**SQLGetInfo**中的下列四個選項描述支援的資料指標類型以及其功能：  
  
-   SQL_CURSOR_SENSITIVITY。 指出資料指標是否對另一個資料指標所做的變更很敏感。  
  
-   SQL_SCROLL_OPTIONS。 列出支援的資料指標類型 (順向、靜態、索引鍵集驅動、動態或混合) 。 所有資料來源都必須支援順向資料指標。  
  
-   SQL_DYNAMIC_CURSOR_ATTRIBUTES1、SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1、SQL_KEYSET_CURSOR_ATTRIBUTES1 或 SQL_STATIC_CURSOR_ATTRIBUTES1 (，視資料指標) 的類型而定。 列出可滾動的資料指標所支援的提取類型。 傳回值中的位會對應至 **SQLFetchScroll**中的提取類型。  
  
-   SQL_KEYSET_CURSOR_ATTRIBUTES2 或 SQL_STATIC_CURSOR_ATTRIBUTES2 (，視資料指標) 的類型而定。 列出靜態和索引鍵集驅動的資料指標是否可以偵測到自己的更新、刪除和插入。  
  
 應用程式可以使用這些選項來呼叫 **SQLGetInfo** ，以判斷執行時間的資料指標功能。 這通常是由一般應用程式所完成。 您也可以在應用程式開發期間判斷資料指標功能，並在應用程式中使用硬式編碼。 這通常是由垂直和自訂的應用程式來完成，但是也可以由使用用戶端資料指標實現（例如 ODBC 資料指標程式庫）的一般應用程式來完成。

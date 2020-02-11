---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 14715e40cd99f3f1a03c2ae19e825705a8376e30
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68040002"
---
# <a name="determining-cursor-capabilities"></a>判斷資料指標的功能
**SQLGetInfo**中的下列四個選項描述支援哪些類型的資料指標，以及其功能為何：  
  
-   SQL_CURSOR_SENSITIVITY。 指出資料指標是否對另一個資料指標所做的變更很敏感。  
  
-   SQL_SCROLL_OPTIONS。 列出支援的資料指標類型（順向、靜態、索引鍵集驅動、動態或混合）。 所有資料來源都必須支援順向資料指標。  
  
-   SQL_DYNAMIC_CURSOR_ATTRIBUTES1、SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1、SQL_KEYSET_CURSOR_ATTRIBUTES1 或 SQL_STATIC_CURSOR_ATTRIBUTES1 （視游標的類型而定）。 列出可滾動資料指標所支援的提取類型。 傳回值中的位會對應到**SQLFetchScroll**中的提取類型。  
  
-   SQL_KEYSET_CURSOR_ATTRIBUTES2 或 SQL_STATIC_CURSOR_ATTRIBUTES2 （視游標的類型而定）。 列出靜態和索引鍵集導向的資料指標是否可以偵測自己的更新、刪除和插入。  
  
 應用程式可以藉由使用這些選項呼叫**SQLGetInfo** ，在執行時間判斷資料指標功能。 這通常是由一般應用程式來完成。 資料指標功能也可以在應用程式開發期間決定，並在應用程式中使用硬式編碼。 這通常是由垂直和自訂應用程式所完成，但也可以由使用用戶端資料指標執行的泛型應用程式來完成，例如 ODBC 資料指標程式庫。

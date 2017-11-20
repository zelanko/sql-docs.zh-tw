---
title: "轉譯 Dll |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- translation DLLs [ODBC]
ms.assetid: 38975059-b346-410f-bb27-326f3f7bbf39
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 06e496e3999904a019f481374598a9a774729ab3
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="translation-dlls"></a>轉譯 Dll
通常，應用程式和資料來源會將資料儲存數個不同的字元集。 ODBC 提供讓驅動程式，將資料從一個字元設為另一個轉譯的一般機制。 其中包含實作的轉譯函式之 DLL 的**SQLDriverToDataSource**和**SQLDataSourceToDriver**，呼叫要轉譯資料的資料來源之間傳輸驅動程式和驅動程式。 這個 DLL 可以撰寫應用程式開發人員，驅動程式開發人員，或第三方。  
  
 可以指定特定的資料來源的翻譯 DLL 中該資料來源; 的系統資訊如需詳細資訊，請參閱[資料來源規格子機碼](../../../odbc/reference/install/data-source-specification-subkeys.md)。 它也可以設定在執行階段使用 SQL_ATTR_TRANSLATE_DLL 和 SQL_ATTR_TRANSLATE_OPTION 連接屬性。  
  
 轉譯選項是可以解譯只能由特定的轉譯 DLL 的值。 比方說，如果轉譯 DLL 將不同的字碼頁之間轉譯，選項可能會產生應用程式和資料來源所使用的字碼頁的數字。 沒有要使用的轉譯選項翻譯 DLL 的需求。  
  
 之後在指定 DLL 的翻譯，驅動程式會載入它，並呼叫它來轉譯資料的應用程式和資料來源之間傳輸。 這包含所有 SQL 陳述式以及字元參數傳送到資料來源，並從資料來源擷取的所有字元，例如資料行名稱和錯誤訊息的字元中繼資料。 連線資料不會進行轉譯，因為應用程式已連接到資料來源之後，直到沒有載入轉譯 DLL。


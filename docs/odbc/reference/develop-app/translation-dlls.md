---
title: 轉譯 Dll |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- translation DLLs [ODBC]
ms.assetid: 38975059-b346-410f-bb27-326f3f7bbf39
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ec1d0e23019f3e5b68ad38711c1f041b160ceb31
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63305743"
---
# <a name="translation-dlls"></a>轉譯 DLL
通常，應用程式和資料來源會將資料儲存數個不同的字元集。 ODBC 會提供可讓驅動程式，將資料從一個設為另一個的字元轉譯的一般機制。 其中包含實作的轉譯函式的 DLL **SQLDriverToDataSource**並**SQLDataSourceToDriver**，由將轉譯的資料來源之間流動的所有資料驅動程式呼叫和驅動程式。 這個 DLL 可以寫入應用程式開發人員，驅動程式開發人員，或第三方。  
  
 轉譯 DLL 特定資料來源可以指定該資料來源; 的系統資訊如需詳細資訊，請參閱 <<c0> [ 資料來源規格子機碼](../../../odbc/reference/install/data-source-specification-subkeys.md)。 它也可以設定在執行階段使用 SQL_ATTR_TRANSLATE_DLL 和 SQL_ATTR_TRANSLATE_OPTION 連接屬性。  
  
 轉譯選項是一個可以解譯只能由特定的轉譯 DLL 的值。 比方說，如果轉譯 DLL 將不同的字碼頁之間轉譯，選項可能會讓應用程式和資料來源所使用的字碼頁的數字。 沒有要使用的轉譯選項翻譯 DLL 的需求。  
  
 之後在指定 DLL 的翻譯，驅動程式會載入它，並呼叫它來轉譯應用程式與資料來源之間流動的所有資料。 這包括所有的 SQL 陳述式和字元參數傳送至資料來源，以及從資料來源擷取的所有字元都會、 字元中繼資料，例如資料行名稱和錯誤訊息。 連線資料不會進行轉譯，因為應用程式已連接到資料來源之後，直到沒有載入轉譯 DLL。

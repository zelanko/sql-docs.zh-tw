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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3dad12bcd71434c1013b4fde5b4bd0231e56016f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81297943"
---
# <a name="translation-dlls"></a>轉譯 DLL
應用程式和資料來源通常會將資料儲存在不同的字元集中。 ODBC 提供了一種泛型機制，可讓驅動程式將資料從一個字元集轉譯成另一組。 其中包含的 DLL 會執行轉譯函式**SQLDriverToDataSource**和**SQLDataSourceToDriver**，而驅動程式會呼叫這些函式來轉譯資料來源和驅動程式之間流動的所有資料。 這個 DLL 可以由應用程式開發人員、驅動程式開發人員或協力廠商撰寫。  
  
 特定資料來源的轉譯 DLL 可以在該資料來源的系統資訊中指定;如需詳細資訊，請參閱[資料來源規格](../../../odbc/reference/install/data-source-specification-subkeys.md)子機碼。 您也可以在執行時間使用 SQL_ATTR_TRANSLATE_DLL 和 SQL_ATTR_TRANSLATE_OPTION 連接屬性來設定它。  
  
 翻譯選項是只能由特定轉譯 DLL 來解讀的值。 例如，如果翻譯 DLL 在不同的字碼頁之間轉譯，則選項可能會提供應用程式和資料來源所使用的字碼頁數目。 翻譯 DLL 不需要使用轉譯選項。  
  
 指定翻譯 DLL 之後，驅動程式會將它載入，並呼叫它來轉譯應用程式與資料來源之間流動的所有資料。 這包括所有要傳送到資料來源的 SQL 語句和字元參數，以及所有字元結果、字元中繼資料（例如資料行名稱），以及從資料來源抓取的錯誤訊息。 連接資料不會轉譯，因為在應用程式連接到資料來源之前，不會載入轉譯 DLL。

---
title: 翻譯 DLL |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297943"
---
# <a name="translation-dlls"></a>轉譯 DLL
應用程式和數據源通常將資料存儲在不同的字元集中。 ODBC 提供了一種通用機制,允許驅動程式將數據從一個字元集轉換為另一個字元集。 它由 DLL 組成,它實現了轉換函數**SQLDriverToDataSource**和**SQLDataSourceToDriver,** 驅動程式呼叫它們來轉換資料源和驅動程式之間的所有資料。 此 DLL 可以由應用程式開發人員、驅動程式開發人員或第三方編寫。  
  
 可以在該資料源的系統資訊中指定特定數據源的轉換 DLL;關於詳細資訊,請參考[資料來源規範子金鑰](../../../odbc/reference/install/data-source-specification-subkeys.md)。 也可以在運行時使用SQL_ATTR_TRANSLATE_DLL和SQL_ATTR_TRANSLATE_OPTION連接屬性進行設置。  
  
 翻譯選項是只能由特定翻譯 DLL 解釋的值。 例如,如果轉換 DLL 在不同的代碼頁之間進行轉換,則該選項可能會給出應用程式和數據原始使用的程式碼頁的數量。 無需翻譯 DLL 使用翻譯選項。  
  
 指定轉換 DLL 後,驅動程式將載入它並調用它來轉換應用程式和數據源之間的所有資料。 這包括發送到資料來源的所有 SQL 語句和字元參數,以及所有字元結果、字元資料(如列名)以及從資料來源檢索的錯誤訊息。 連接資料不會翻譯,因為轉換 DLL 直到應用程式連接到數據源後才會載入。

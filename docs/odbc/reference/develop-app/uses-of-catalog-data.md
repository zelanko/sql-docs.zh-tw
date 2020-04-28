---
title: 目錄資料的使用 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog data [ODBC]
- functions [ODBC], catalog functions
- catalog functions [ODBC], using catalog data
ms.assetid: d5915d0c-eec3-4382-850e-bd863763c99a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 429d42d4a82d0f9f34e33eb4f5f3293100505da9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306809"
---
# <a name="uses-of-catalog-data"></a>使用目錄資料
應用程式會以各種不同的方式使用目錄資料。 以下是一些常見的用法：  
  
-   **在執行時間建立 SQL 語句。** 垂直應用程式（例如訂單輸入應用程式）包含硬式編碼的 SQL 語句。 應用程式所使用的資料表和資料行會在一段時間內固定，如同存取這些資料表的語句。 例如，訂單輸入應用程式通常會包含單一的參數化**INSERT**語句，以便將新訂單加入系統中。  
  
     一般應用程式，例如使用 ODBC 來抓取資料的試算表程式，通常會根據使用者的輸入，在執行時間建立 SQL 語句。 這類應用程式可能會要求使用者輸入要使用之資料表和資料行的名稱。 不過，如果應用程式顯示的是資料表和資料行的清單，而使用者可以從中進行選取，則使用者會更容易。 若要建立這些清單，應用程式會呼叫**SQLTables**和**SQLColumns**目錄函數。  
  
-   **在開發期間建立 SQL 語句。** 應用程式開發環境通常可讓程式設計師在開發程式時建立資料庫查詢。 然後，查詢會在所建立的應用程式中進行硬式編碼。  
  
     這類環境也可以使用**SQLTables**和**SQLColumns**來建立程式設計人員可以從中進行選擇的清單。 這些環境也可能會使用**SQLPrimaryKeys**和**SQLForeignKeys**自動判斷和顯示所選資料表之間的關聯性，並使用**SQLStatistics**來判斷和反白顯示索引欄位，讓程式設計人員能夠建立有效率的查詢。  
  
-   **建立資料指標。** 提供可滾動資料指標引擎的應用程式、驅動程式或中介軟體，可以使用**SQLSpecialColumns**來判斷唯一識別資料列的資料行。 此程式可以建立一個索引*鍵集*，其中包含每個已提取資料列的這些資料行的值。 當應用程式回復至資料列時，它會使用這些值來提取資料列的最新資料。 如需可滾動資料指標和索引鍵集的詳細資訊，請參閱可滾動的資料[指標](../../../odbc/reference/develop-app/scrollable-cursors.md)。

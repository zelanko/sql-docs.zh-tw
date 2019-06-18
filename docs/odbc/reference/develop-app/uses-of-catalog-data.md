---
title: 使用目錄資料 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d9b75d59d8fc28e364f5826d95e7fc50cb6afda7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63312526"
---
# <a name="uses-of-catalog-data"></a>使用目錄資料
應用程式會使用目錄資料的各種不同的方式。 以下是一些常見的用法：  
  
-   **在執行階段建構 SQL 陳述式。** 垂直應用程式，例如訂單輸入應用程式中，包含硬式編碼的 SQL 陳述式。 資料表和應用程式所使用的資料行被固定的預先完成，因為存取這些資料表的陳述式。 例如，訂單輸入應用程式通常包含單一參數化**插入**陳述式將新訂單加入至系統。  
  
     泛型應用程式，例如試算表程式，以使用 ODBC 擷取資料，通常會在根據使用者輸入的執行階段建構 SQL 陳述式。 這類應用程式可能需要使用者輸入的資料表和資料行使用的名稱。 不過，它會讓使用者更容易如果應用程式顯示的資料表和使用者可以從中進行選擇的資料行的清單。 若要建立這些清單，應用程式可以呼叫**SQLTables**並**SQLColumns**目錄函式。  
  
-   **在開發期間建構 SQL 陳述式。** 應用程式開發環境中通常會讓程式設計師開發程式時建立資料庫查詢。 查詢接著會硬式編碼所建置的應用程式。  
  
     也可以使用這類環境**SQLTables**並**SQLColumns**建立程式設計人員無法從中進行選擇的清單。 這些環境可能也會使用**SQLPrimaryKeys**並**SQLForeignKeys**自動判斷和顯示選定的資料表之間的關聯性，並使用**SQLStatistics**判斷，並讓程式設計人員可以建立有效率的查詢，將索引的欄位反白顯示。  
  
-   **建構資料指標。** 可以使用應用程式、 驅動程式或提供可捲動資料指標引擎的中介軟體**SQLSpecialColumns**來判斷哪些資料行或資料行可唯一識別資料列。 程式可以建置*keyset*包含每個資料列，擷取這些資料行的值。 當應用程式捲動回到資料列時，它會來提取資料列的最新資料，然後使用這些值。 如需有關可捲動資料指標和索引鍵集的詳細資訊，請參閱 <<c0> [ 可捲動資料指標](../../../odbc/reference/develop-app/scrollable-cursors.md)。

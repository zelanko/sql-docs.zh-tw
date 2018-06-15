---
title: 使用的目錄資料 |Microsoft 文件
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
- catalog data [ODBC]
- functions [ODBC], catalog functions
- catalog functions [ODBC], using catalog data
ms.assetid: d5915d0c-eec3-4382-850e-bd863763c99a
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b4d510a0f7e0d0c401e0f8ea8a8c346a917f05c3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32915243"
---
# <a name="uses-of-catalog-data"></a>目錄資料的使用
應用程式會使用各種方式的類別目錄資料。 以下是一些常見用法：  
  
-   **在執行階段建構 SQL 陳述式。** 垂直應用程式，例如訂單輸入應用程式中，包含硬式編碼的 SQL 陳述式。 資料表和應用程式所使用的資料行被固定的工作量，以存取這些資料表的陳述式。 例如，訂單輸入應用程式通常會包含單一參數化**插入**陳述式，將系統中加入新的訂單。  
  
     泛型應用程式，例如使用 ODBC 擷取資料、 試算表程式通常會在執行階段根據使用者輸入建構 SQL 陳述式。 這類應用程式可能需要使用者輸入的資料表和要使用資料行的名稱。 不過，它可讓使用者更容易如果應用程式顯示的資料表和使用者無法從中進行選擇的資料行清單。 若要建立這些清單，應用程式可以呼叫**SQLTables**和**SQLColumns**目錄函數。  
  
-   **在開發期間建構 SQL 陳述式。** 應用程式開發環境通常可讓程式設計人員開發程式時建立資料庫查詢。 此查詢然後是硬式編碼所建置的應用程式中。  
  
     也可以使用這類環境**SQLTables**和**SQLColumns**建立程式設計人員無法從中進行選擇的清單。 也可能會使用這些環境**SQLPrimaryKeys**和**SQLForeignKeys**自動判斷，顯示選定的資料表之間的關聯性，並使用**SQLStatistics**判斷，並讓程式設計人員可以建立有效率的查詢，將索引的欄位反白顯示。  
  
-   **建構資料指標。** 應用程式、 驅動程式或中介軟體提供可捲動資料指標引擎，可以使用**SQLSpecialColumns**來判斷哪些資料行或資料行可唯一識別資料列。 程式無法建立*索引鍵集*包含每個資料列已經提取這些資料行的值。 當應用程式將捲動回資料列時，它會擷取最新的資料列，然後使用這些值。 如需可捲動資料指標和索引鍵集的詳細資訊，請參閱[可捲動資料指標](../../../odbc/reference/develop-app/scrollable-cursors.md)。

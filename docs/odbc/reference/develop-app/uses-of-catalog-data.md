---
description: 使用目錄資料
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
ms.openlocfilehash: 7e03dff0a8c5715a86f1bcdff65b74f55409889a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471195"
---
# <a name="uses-of-catalog-data"></a>使用目錄資料
應用程式會以各種不同的方式使用目錄資料。 以下是一些常見的用法：  
  
-   **在執行時間建立 SQL 語句。** 垂直的應用程式（例如訂單輸入應用程式）包含硬式編碼的 SQL 語句。 應用程式所使用的資料表和資料行會事先修正，就像存取這些資料表的語句一樣。 例如，訂單輸入應用程式通常會包含單一的參數化 **INSERT** 語句，以將新的訂單新增至系統。  
  
     一般應用程式，例如使用 ODBC 抓取資料的試算表程式，通常會根據使用者的輸入，在執行時間建立 SQL 語句。 這類應用程式可能會要求使用者輸入要使用的資料表和資料行名稱。 但是，如果應用程式所顯示的資料表和資料行清單讓使用者可以進行選取，就會比較容易。 若要建立這些清單，應用程式會呼叫 **SQLTables** 和 **SQLColumns** 目錄函數。  
  
-   **在開發期間建立 SQL 語句。** 應用程式開發環境通常可讓程式設計師在開發程式時建立資料庫查詢。 然後，查詢會在所建立的應用程式中硬式編碼。  
  
     這類環境也可以使用 **SQLTables** 和 **SQLColumns** 來建立程式設計師可以從中進行選擇的清單。 這些環境可能也會使用 **SQLPrimaryKeys** 和 **SQLForeignKeys** 來自動判斷並顯示所選資料表之間的關聯性，並使用 **SQLStatistics** 來判斷和醒目提示索引欄位，讓程式設計人員能夠建立有效率的查詢。  
  
-   **建立資料指標。** 提供可滾動資料指標引擎的應用程式、驅動程式或中介軟體可以使用 **SQLSpecialColumns** 來判斷哪個資料行可唯一識別資料列。 此程式可以針對每個已提取的資料列，建立包含這些資料行值的索引 *鍵集* 。 當應用程式回復至資料列時，它會接著使用這些值來提取資料列的最新資料。 如需可滾動資料指標和索引鍵集的詳細資訊，請參閱可滾動的資料 [指標](../../../odbc/reference/develop-app/scrollable-cursors.md)。

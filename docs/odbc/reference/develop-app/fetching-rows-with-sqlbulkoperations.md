---
title: 使用 SQLBulk 操作提取行 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data updates [ODBC], bookmarks
- SQLBulkOperations function [ODBC], fetching rows
- data updates [ODBC], SQLBulkOperations
- bookmarks [ODBC]
- updating data [ODBC], bookmarks
- updating data [ODBC], SQLBulkOperations
ms.assetid: 0efee2d6-ce94-411e-9976-97ba28b8da37
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ae0b4c2114059cecaaf8f8825169300f131bd473
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305647"
---
# <a name="fetching-rows-with-sqlbulkoperations"></a>使用 SQLBulkOperations 擷取資料列
可以通過調用**SQLBulk 操作**將數據重新提取到行集中。 要提取的行由綁定書簽列中的書籤標識。 不提取值為SQL_COLUMN_IGNORE的列。  
  
 要使用**SQLBulk 執行**大量擷取,應用程式執行以下操作:  
  
1.  檢索並緩存要更新的所有行的書籤。 如果有多個書籤和按列綁定,則書簽存儲在陣列中;如果使用多個書籤和按列綁定,則書籤將存儲在陣列中。如果有多個書籤和逐行綁定,則書簽存儲在行結構陣組中。  
  
2.  將SQL_ATTR_ROW_ARRAY_SIZE語句屬性設置為要提取的行數,並將包含書籤值的緩衝區或書籤陣列綁定到列 0。  
  
3.  根據需要設置每列的長度/指示器緩衝區中的值。 這是數據或SQL_NTS的位元組長度,用於綁定到字串緩衝區的列、綁定到二進位緩衝區的列的數據字節長度,以及要設置為NULL的任何列SQL_NULL_DATA。 應用程式將要設置為預設(如果存在)或 NULL(如果不存在)的列的長度/指示器緩衝區中的值設置為SQL_COLUMN_IGNORE。  
  
4.  呼叫**SQLBulk 操作**,*操作*參數設定為SQL_FETCH_BY_BOOKMARK。  
  
 應用程式無需使用行操作陣組來防止對某些列執行操作。 應用程式通過僅將這些行的書籤複製到綁定書籤陣列來選擇要獲取的行。

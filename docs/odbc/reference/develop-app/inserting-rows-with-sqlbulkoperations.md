---
title: 使用 SQLBulk 操作插入行 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBulkOperations function [ODBC], inserting rows
- data updates [ODBC], SQLBulkOperations
- updating data [ODBC], SQLBulkOperations
ms.assetid: ed585ea7-4d56-4df9-8dc3-53ca82382450
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a6fa384292f02026b8390aa92525144dce6f549b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300108"
---
# <a name="inserting-rows-with-sqlbulkoperations"></a>使用 SQLBulkOperations 插入資料列
使用**SQLBulk 操作**插入數據類似於使用**SQLBulk 操作**更新數據,因為它使用綁定應用程式緩衝區中的數據。  
  
 因此,新行中的每個列都有一個值,所有長度/指示器值為 SQL_COLUMN_IGNORE的綁定列都必須接受 NULL 值或具有預設值。  
  
 若要使用**SQLBulk 操作**插入行,應用程式執行以下操作:  
  
1.  將SQL_ATTR_ROW_ARRAY_SIZE語句屬性設置為要插入的行數,並將新資料值放在綁定的應用程序緩衝區中。 有關如何使用**SQLBulk 操作**傳送長資料的資訊,請參閱[長資料和 SQLSetPos 和 SQLBulk 操作](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)。  
  
2.  根據需要設置每列的長度/指示器緩衝區中的值。 這是數據或SQL_NTS的位元組長度,用於綁定到字串緩衝區的列、綁定到二進位緩衝區的列的數據字節長度,以及要設置為NULL的任何列SQL_NULL_DATA。 應用程式將要設置為預設(如果存在)或 NULL(如果不存在)的列的長度/指示器緩衝區中的值設置為SQL_COLUMN_IGNORE。  
  
3.  使用設定為SQL_ADD*的操作*參數呼叫**SQLBulk 操作**。  
  
 **SQLBulk 操作**傳回後,當前行將保持不變。 如果綁定書籤列(列**0),SQLBulk 操作**將返回綁定到該列的行集緩衝區中插入的行的書籤。

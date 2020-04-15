---
title: 使用 SQLBulk 操作按書籤刪除行 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data updates [ODBC], SQLBulkOperations
- SQLBulkOperations function [ODBC], deleting rows
- updating data [ODBC], SQLBulkOperations
ms.assetid: 46139ec9-7095-481a-bf45-20200a2fdc03
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6b6a4c1b24ee276c86175392eb45ac5ce0aa45e5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305959"
---
# <a name="deleting-rows-by-bookmark-with-sqlbulkoperations"></a>使用 SQLBulkOperations 依書籤刪除資料列
按書籤刪除行時 **,SQLBulk操作**使數據源刪除表的一個或多個選定行。 行由綁定書簽列中的書籤標識。  
  
 要使用**SQLBulk 來透過**書籤刪除行,應用程式執行以下操作:  
  
1.  檢索並快取要刪除的所有行的書籤。 如果有多個書籤和按列綁定,則書簽存儲在陣列中;如果使用多個書籤和按列綁定,則書籤將存儲在陣列中。如果有多個書籤和逐行綁定,則書簽存儲在行結構陣組中。  
  
2.  將SQL_ATTR_ROW_ARRAY_SIZE語句屬性設置為書籤數,並將包含書籤值的緩衝區或書籤陣列綁定到列 0。  
  
3.  將**SQLBulk 操作***設置為SQL_DELETE_BY_BOOKMARK。*

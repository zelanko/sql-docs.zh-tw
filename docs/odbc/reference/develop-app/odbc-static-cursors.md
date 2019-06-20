---
title: ODBC 靜態資料指標 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], static
- static cursors [ODBC]
ms.assetid: 28cb324c-e1c3-4b5c-bc3e-54df87037317
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8ddd2b4d998ab2718757db4dd58de6aea8bee05e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62799014"
---
# <a name="odbc-static-cursors"></a>ODBC 靜態資料指標
靜態資料指標是其中一個結果集似乎是靜態。 它通常無法偵測到的成員資格、 順序或結果集資料指標開啟後的值所做的變更。 例如，假設在靜態資料指標提取資料列和另一個應用程式，然後更新該資料列。 如果靜態資料指標 refetches 資料列，則它所看到的值會是不變，即使由其他應用程式所做的變更。  
  
 靜態資料指標可以偵測到自己的更新、 刪除和插入，雖然不需要執行這項操作。 透過 SQL_STATIC_SENSITIVITY 選項中是否有特定的靜態資料指標偵測這些變更回報**SQLGetInfo**。 靜態資料指標永遠不會偵測其他更新、 刪除和插入。  
  
 Sql_attr_row_status_ptr 設定陳述式屬性所指定之資料列狀態陣列可以包含 SQL_ROW_SUCCESS、 SQL_ROW_SUCCESS_WITH_INFO 或 SQL_ROW_ERROR 的任何資料列。 它會傳回 SQL_ROW_UPDATED、 SQL_ROW_DELETED 或 SQL_ROW_ADDED 更新、 刪除或插入游標處，假設資料指標可以偵測這類變更的資料列。  
  
 靜態資料指標通常會實作藉由鎖定結果集的資料列，或藉由複製，或快照集，結果的設定。 雖然鎖定資料列是很簡單，它會有大幅降低並行的缺點。 製作複本允許更高的並行處理和可讓資料指標來追蹤它自己的更新、 刪除和插入所修改該複本。 不過，複本會耗費更多資源並為該資料其他人已變更，可以偏離基礎資料。

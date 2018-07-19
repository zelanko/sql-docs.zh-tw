---
title: ODBC 靜態游標 |Microsoft 文件
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
- cursors [ODBC], static
- static cursors [ODBC]
ms.assetid: 28cb324c-e1c3-4b5c-bc3e-54df87037317
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b2ee8c5945e3ebed86df370fd537f9bc543ce844
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32910903"
---
# <a name="odbc-static-cursors"></a>ODBC 靜態游標
靜態資料指標是其中一個結果集似乎是靜態。 它通常無法偵測到的成員資格、 順序或值之結果集資料指標開啟後所做的變更。 例如，假設在靜態資料指標提取的資料列，而另一個應用程式，然後再更新該資料列。 如果靜態資料指標 refetches 資料列，它會看到的值是不變，即使其他應用程式所做的變更。  
  
 靜態資料指標可以偵測到自己的更新、 刪除和插入，雖然不需要執行這項操作。 透過 SQL_STATIC_SENSITIVITY 選項中是否有特定的靜態資料指標偵測到這些變更會報告**SQLGetInfo**。 靜態資料指標永遠不會偵測其他更新、 刪除和插入。  
  
 將 sql_attr_row_status_ptr 設定陳述式屬性所指定之資料列狀態陣列可以包含 SQL_ROW_SUCCESS、 SQL_ROW_SUCCESS_WITH_INFO 或 SQL_ROW_ERROR 的任何資料列。 它會傳回 SQL_ROW_UPDATED、 SQL_ROW_DELETED 或 SQL_ROW_ADDED 更新、 刪除或插入游標處，假設資料指標可以偵測到這類變更的資料列。  
  
 通常實作以鎖定的結果集的資料列，或藉由複製，或快照集，結果集的靜態資料指標。 雖然鎖定資料列是相當容易，但是它有大幅降低並行的缺點。 建立複本允許更大的並行存取可讓資料指標來追蹤它自己的更新、 刪除和插入所修改該複本。 不過，複本是成本更高時進行，並依照該資料會變更其他人可以分離的基礎資料中。

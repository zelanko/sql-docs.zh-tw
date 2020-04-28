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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b99566c473e88684e8b092a5ac9fc899e7dce177
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81282440"
---
# <a name="odbc-static-cursors"></a>ODBC 靜態資料指標
靜態資料指標是結果集似乎是靜態的。 在開啟資料指標之後，它通常不會偵測到結果集的成員資格、順序或值所做的變更。 例如，假設靜態資料指標提取一個資料列，然後另一個應用程式更新該資料列。 如果靜態資料指標 refetches 資料列，則不論另一個應用程式所做的變更為何，它所看到的值都會保持不變。  
  
 靜態資料指標可以偵測自己的更新、刪除和插入，但不需要這麼做。 特定靜態資料指標是否偵測到這些變更是透過**SQLGetInfo**中的 SQL_STATIC_SENSITIVITY 選項來報告。 靜態資料指標永遠不會偵測到其他更新、刪除和插入。  
  
 SQL_ATTR_ROW_STATUS_PTR 語句屬性所指定的資料列狀態陣列可以包含任何資料列的 SQL_ROW_SUCCESS、SQL_ROW_SUCCESS_WITH_INFO 或 SQL_ROW_ERROR。 它會針對資料指標所更新、刪除或插入的資料列，傳回 SQL_ROW_UPDATED、SQL_ROW_DELETED 或 SQL_ROW_ADDED，假設資料指標可以偵測這類變更。  
  
 靜態資料指標通常是藉由鎖定結果集內的資料列，或製作結果集的複本或快照集來執行。 雖然鎖定資料列相當容易，但它具有大幅減少並行的缺點。 建立複本可提供更高的平行存取權，並可讓游標藉由修改複本來追蹤自己的更新、刪除和插入。 不過，複製的成本較高，而且可以與基礎資料分離，因為其他人會變更資料。

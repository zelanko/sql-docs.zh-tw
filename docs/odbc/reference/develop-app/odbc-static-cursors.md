---
description: ODBC 靜態資料指標
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
ms.openlocfilehash: 9689badd39e21f82c268be904b29ffb1fa90a8ae
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429160"
---
# <a name="odbc-static-cursors"></a>ODBC 靜態資料指標
靜態資料指標是結果集看似靜態的資料指標。 它通常不會偵測在開啟資料指標之後，對結果集的成員資格、順序或值所做的變更。 例如，假設靜態資料指標提取資料列，而另一個應用程式接著更新該資料列。 如果靜態資料指標 refetches 資料列，不論其他應用程式所做的變更為何，它所看到的值都不會變更。  
  
 靜態資料指標可以偵測到它們自己的更新、刪除和插入，不過不需要這麼做。 特定靜態資料指標是否會偵測到這些變更會透過 **SQLGetInfo**中的 SQL_STATIC_SENSITIVITY 選項回報。 靜態資料指標絕對不會偵測到其他更新、刪除和插入。  
  
 SQL_ATTR_ROW_STATUS_PTR 語句屬性指定的資料列狀態陣列可以包含任何資料列的 SQL_ROW_SUCCESS、SQL_ROW_SUCCESS_WITH_INFO 或 SQL_ROW_ERROR。 它會針對資料指標所更新、刪除或插入的資料列，傳回 SQL_ROW_UPDATED、SQL_ROW_DELETED 或 SQL_ROW_ADDED，並假設資料指標可以偵測到這類變更。  
  
 靜態資料指標通常是藉由鎖定結果集中的資料列，或是建立結果集的複本或快照集來執行。 雖然鎖定資料列相當簡單，但它具有大幅減少並行的缺點。 製作複本可提供更大的平行存取，並可讓游標藉由修改複製來追蹤自己的更新、刪除和插入。 不過，複製的成本較高，而且可能會與基礎資料分離，因為其他人會變更該資料。

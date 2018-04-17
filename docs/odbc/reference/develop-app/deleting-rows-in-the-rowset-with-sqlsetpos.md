---
title: 刪除資料列中的資料列集與 SQLSetPos |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLSetPos function [ODBC], deleting rows
- updating data [ODBC], SQLSetPos
- data updates [ODBC], SQLSetPos
ms.assetid: 3117a47d-e179-4f76-89d0-656582f1c9bb
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 828ab8f154669473a6e90b60126d3b047c45e515
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="deleting-rows-in-the-rowset-with-sqlsetpos"></a>SQLSetPos 與資料列集刪除資料列
刪除作業的**SQLSetPos** ，使得資料來源刪除一或多個選取的資料列的資料表。 若要刪除的資料列**SQLSetPos**，應用程式會呼叫**SQLSetPos**與*作業*設定為 SQL_DELETE 並*RowNumber*設為若要刪除的資料列數。 如果*RowNumber*是 0，則會刪除資料列集中的所有資料列。  
  
 之後**SQLSetPos**傳回時，將已刪除的資料列是目前的資料列，而且其狀態為 SQL_ROW_DELETED。 資料列不能用於任何進一步定位作業，例如呼叫**SQLGetData**或**SQLSetPos**。  
  
 刪除資料列集的所有資料列時 (*RowNumber*等於 0)，應用程式可以避免驅動程式刪除某些資料列所使用的資料列作業陣列中的更新作業一樣**SQLSetPos**. (請參閱[SQLSetPos 以更新資料列集中的資料列](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)。)  
  
 刪除的每一個資料列都應該是存在於結果集內的資料列。 如果應用程式緩衝區填滿所擷取，而且已受到維護資料列狀態陣列，其在每個資料列位置的值不應該為 SQL_ROW_DELETED、 SQL_ROW_ERROR 或 SQL_ROW_NOROW。

---
description: 使用 SQLSetPos 刪除資料列集中的資料列
title: 使用 SQLSetPos 刪除資料列集中的資料列 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetPos function [ODBC], deleting rows
- updating data [ODBC], SQLSetPos
- data updates [ODBC], SQLSetPos
ms.assetid: 3117a47d-e179-4f76-89d0-656582f1c9bb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 42b61aa9af15526420b6f2d4ef7e8c945e0da105
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476770"
---
# <a name="deleting-rows-in-the-rowset-with-sqlsetpos"></a>使用 SQLSetPos 刪除資料列集中的資料列
**SQLSetPos**的刪除作業會讓資料來源刪除資料表的一或多個選取的資料列。 若要使用 **SQLSetPos**刪除資料列，應用程式會呼叫 **SQLSetPos** ，並將 *Operation* 設定為 SQL_DELETE，並將 *RowNumber* 設定為要刪除的資料列編號。 如果 *RowNumber* 是0，則會刪除資料列集中的所有資料列。  
  
 **SQLSetPos**傳回之後，已刪除的資料列會是目前的資料列，且其狀態會是 SQL_ROW_DELETED。 資料列不能用於任何進一步的定位作業，例如對 **SQLGetData** 或 **SQLSetPos**的呼叫。  
  
 刪除資料列集的所有資料列時 (*RowNumber* 等於 0) ，應用程式可以使用資料列作業陣列來防止驅動程式刪除某些資料列，方法與 **SQLSetPos**的更新作業一樣。  (參閱 [使用 SQLSetPos 來更新資料列集中的資料列](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)。 )   
  
 刪除的每一個資料列都應該是存在於結果集內的資料列。 如果應用程式緩衝區是藉由提取來填滿，且資料列狀態陣列已維持，則在這些資料列位置的值不應為 SQL_ROW_DELETED、SQL_ROW_ERROR 或 SQL_ROW_NOROW。

---
title: 刪除資料列集中的資料列集使用 SQLSetPos |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 78ee14838b467cfe6e555c97f1e74c65cccf98ff
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47664115"
---
# <a name="deleting-rows-in-the-rowset-with-sqlsetpos"></a>使用 SQLSetPos 刪除資料列集中的資料列
刪除作業**SQLSetPos**刪除一或多個選取的資料列的資料表的資料來源。 若要刪除的資料列**SQLSetPos**，應用程式會呼叫**SQLSetPos**具有*作業*設定為 SQL_DELETE 並*RowNumber*設為若要刪除的資料列數目。 如果*RowNumber*是 0，則會刪除資料列集中的所有資料列。  
  
 在後**SQLSetPos**傳回刪除的資料列是目前的資料列，而且其狀態為 SQL_ROW_DELETED。 資料列不能在任何進一步定位作業，例如呼叫**SQLGetData**或是**SQLSetPos**。  
  
 刪除資料列集的所有資料列時 (*RowNumber*等於 0)，應用程式可以避免驅動程式刪除某些資料列更新作業的相同方式使用資料列作業陣列， **SQLSetPos**. (請參閱[使用 SQLSetPos 更新資料列集中的資料列](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)。)  
  
 刪除的每一個資料列都應該是存在於結果集內的資料列。 如果應用程式緩衝區已填滿所擷取，而且已受到維護的資料列狀態陣列，其在每個資料列位置的值不應該為 SQL_ROW_DELETED、 SQL_ROW_ERROR 或 SQL_ROW_NOROW。

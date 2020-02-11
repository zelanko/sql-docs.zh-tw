---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e39b70f92f7b239b011cdd4fdd6abd36c27561c2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68076798"
---
# <a name="deleting-rows-in-the-rowset-with-sqlsetpos"></a>使用 SQLSetPos 刪除資料列集中的資料列
**SQLSetPos**的 delete 作業會使資料來源刪除資料表的一個或多個選取資料列。 若要使用**SQLSetPos**刪除資料列，應用程式會呼叫**SQLSetPos** ，並將*Operation*設定為 SQL_DELETE 並將*RowNumber*設定為要刪除的資料列數目。 如果*RowNumber*是0，則會刪除資料列集中的所有資料列。  
  
 **SQLSetPos**傳回之後，刪除的資料列就是目前的資料列，而且其狀態會是 SQL_ROW_DELETED。 資料列無法用於任何進一步的定位作業，例如呼叫**SQLGetData**或**SQLSetPos**。  
  
 刪除資料列集的所有資料列（*RowNumber*等於0）時，應用程式可以使用資料列作業陣列防止驅動程式刪除特定資料列，方法與**SQLSetPos**的更新作業相同。 （請參閱[使用 SQLSetPos 更新資料列集中](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)的資料列）。  
  
 刪除的每一個資料列都應該是存在於結果集內的資料列。 如果應用程式緩衝區已藉由提取填滿，而且如果已維護資料列狀態陣列，則每個資料列位置的值都不應該 SQL_ROW_DELETED、SQL_ROW_ERROR 或 SQL_ROW_NOROW。

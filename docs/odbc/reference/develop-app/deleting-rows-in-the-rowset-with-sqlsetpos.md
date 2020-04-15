---
title: 使用 SQLSetPos 刪除行 :微軟文件
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
ms.openlocfilehash: 940bcc3e2ee6a042394797d6038028cce64862f1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305949"
---
# <a name="deleting-rows-in-the-rowset-with-sqlsetpos"></a>使用 SQLSetPos 刪除資料列集中的資料列
**SQLSetPos**的刪除操作使數據源刪除表的一個或多個選定行。 要刪除**SQLSetPos 的**行,應用程式呼叫**SQLSetPos,***操作*設定為SQL_DELETE,*行號*設定為要刪除的行數。 如果*RowNumber*為 0,則刪除行集中的所有行。  
  
 **SQLSetPos**傳回後,已刪除的行是當前行,其狀態為SQL_ROW_DELETED。 該行不能用於任何進一步的定位操作,例如對**SQLGetData**或**SQLSetPos**的調用。  
  
 刪除列集的所有*行號*等於 0)時,應用程式可以阻止驅動程式使用行操作陣列刪除某些行,其方式與**SQLSetPos**的更新操作相同。 (請參閱[使用 SQLSetPos 更新行。](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)  
  
 刪除的每一個資料列都應該是存在於結果集內的資料列。 如果應用程式緩衝區是通過提取填充的,並且已維護行狀態陣列,則不應SQL_ROW_DELETED、SQL_ROW_ERROR或SQL_ROW_NOROW這些行位置的值。

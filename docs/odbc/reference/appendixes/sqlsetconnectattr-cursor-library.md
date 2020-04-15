---
title: SQLSetConnectAttr(游標庫) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectAttr function [ODBC], Cursor Library
ms.assetid: 6f70bbd0-a057-49ef-8b05-4c80b58fc6e6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a87c85d727fb9eb2fc27613b9eecd3fe0ec51b58
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300538"
---
# <a name="sqlsetconnectattr-cursor-library"></a>SQLSetConnectAttr (資料指標程式庫)
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 避免在新的開發工作中使用此功能,並計劃修改當前使用此功能的應用程式。 Microsoft 建議使用驅動程式的游標功能。  
  
 本主題討論在遊標庫中使用**SQLSetConnect Attr**函數。 有關**SQLSetConnectAttr**的一般資訊,請參閱[SQLSetConnectAttr 函數](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)。  
  
 應用程式使用SQL_ATTR_ODBC_CURSORS屬性調用**SQLSetConnectAttr,** 以指定是否始終使用游標庫、驅動程式不支援可滾動遊標或從未使用過。 游標庫假定驅動程式支援可滾動遊標,如果它返回 SQL_CA1_RELATIVE在**SQLGetInfo**中SQL_STATIC_CURSOR_ATTRIBUTES1資訊類型。  
  
 應用程式必須調用**SQLSetConnectAttr**來指定使用 SQLAllocHandle 的遊標庫使用方式,在調用**SQLAllocHandle**時,它使用 SQL_HANDLE_DBC*的句柄類型*來分配連接,然後再連接到數據來源。 如果應用程式在連接仍處於活動狀態時使用 SQL_ATTR_ODBC_CURSORS 屬性調用**SQLSetConnectAttr,** 則游標庫將返回錯誤。  
  
 要為與連接關聯的所有語句設置游標庫支援的語句屬性,應用程式必須在連接到數據源並在打開遊標之前為該語句屬性調用**SQLSetConnectAttr。** 如果應用程式使用語句屬性調用**SQLSetConnectAttr,** 並且與連接關聯的語句上打開游標,則在關閉和重新打開遊標之前,語句屬性將不會應用於該語句。

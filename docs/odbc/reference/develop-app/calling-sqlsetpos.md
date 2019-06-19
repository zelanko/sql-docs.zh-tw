---
title: Calling SQLSetPos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], SQLSetPos
- SQLSetPos function [ODBC], calling
- upgrading applications [ODBC], SQLSetPos
- backward compatibility [ODBC], SqlSetPos
- application upgrades [ODBC], SQLSetPos
ms.assetid: 846354b8-966c-4c2c-b32f-b0c8e649cedd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 70d574f867934af87ac7b5071b7f30bc9e89bccf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63199443"
---
# <a name="calling-sqlsetpos"></a>呼叫 SQLSetPos
在 ODBC 2。*x*，資料列狀態陣列的指標是引數**SQLExtendedFetch**。 藉由呼叫稍後更新資料列狀態陣列**SQLSetPos**。 有些驅動程式有依賴這個陣列不會變更之間的事實**SQLExtendedFetch**並**SQLSetPos**。 在 ODBC 3。*x*狀態陣列的指標是描述項欄位，因此應用程式可以輕鬆地將它變更為指向不同的陣列。 這可以是 ODBC 3 時發生問題。*x*應用程式正在使用的 ODBC 2。*x*驅動程式會呼叫，但**SQLSetStmtAttr**陣列狀態指標設定，然後會呼叫**SQLFetchScroll**來提取資料。 驅動程式管理員會將它對應為一連串的呼叫**SQLExtendedFetch**。 下列程式碼會通常會引發錯誤時，驅動程式管理員會對應第二個**SQLSetStmtAttr**使用 ODBC 2 時呼叫 *.x*驅動程式：  
  
```  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, rgfRowStatus, 0);  
SQLFetchScroll(hstmt, fFetchType, iRow);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, rgfRowStat1, 0);  
SQLSetPos(hstmt, iRow, fOption, fLock);  
```  
  
 如果沒有任何方法可以變更資料列狀態指標，ODBC 2 中的，就會引發錯誤。*x*呼叫之間**SQLExtendedFetch**。 相反地，驅動程式管理員時，執行下列步驟使用 ODBC 2 *.x*驅動程式：  
  
1.  初始化內部的驅動程式管理員旗標*fSetPosError*設為 TRUE。  
  
2.  當應用程式呼叫**SQLFetchScroll**，驅動程式管理員會將*fSetPosError*為 FALSE。  
  
3.  當應用程式呼叫**SQLSetStmtAttr**若要設定 sql_attr_row_status_ptr 設定，驅動程式管理員會將*fSetPosError*等於 toTRUE。  
  
4.  當應用程式呼叫**SQLSetPos**，以*fSetPosError*等於 TRUE，則驅動程式管理員會產生 sql_error，其中包含 SQLSTATE HY011 （屬性現在無法設定），表示應用程式嘗試呼叫**SQLSetPos**之後變更資料列狀態指標，但在呼叫之前**SQLFetchScroll**。

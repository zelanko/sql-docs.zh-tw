---
title: 呼叫 SQLSetPos |Microsoft 文件
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
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], SQLSetPos
- SQLSetPos function [ODBC], calling
- upgrading applications [ODBC], SQLSetPos
- backward compatibility [ODBC], SqlSetPos
- application upgrades [ODBC], SQLSetPos
ms.assetid: 846354b8-966c-4c2c-b32f-b0c8e649cedd
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1c34e1e5f9c4dae5f2a39cadd6b9afbdc03403b5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="calling-sqlsetpos"></a>呼叫 SQLSetPos
在 ODBC 2。*x*，資料列狀態陣列的指標是以引數**SQLExtendedFetch**。 呼叫更新版本已更新資料列狀態陣列**SQLSetPos**。 有些驅動程式有依賴這個陣列不會變更之間的事實**SQLExtendedFetch**和**SQLSetPos**。 在 ODBC 3。*x*狀態陣列的指標是描述項欄位，因此應用程式可以輕鬆地將它變更為指向不同的陣列。 這可以是 ODBC 3 時的問題。*x*應用程式使用 ODBC 2。*x*驅動程式，但呼叫**SQLSetStmtAttr**陣列狀態指標設定，然後會呼叫**SQLFetchScroll**來提取資料。 驅動程式管理員將它對應為一連串的呼叫**SQLExtendedFetch**。 下列程式碼，就通常會引發錯誤時，驅動程式管理員會將對應第二個**SQLSetStmtAttr**使用 ODBC 2 時呼叫 *.x*驅動程式：  
  
```  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, rgfRowStatus, 0);  
SQLFetchScroll(hstmt, fFetchType, iRow);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, rgfRowStat1, 0);  
SQLSetPos(hstmt, iRow, fOption, fLock);  
```  
  
 如果沒有任何方法可變更 ODBC 2 中的資料列狀態指標，就會引發錯誤。*x*呼叫之間**SQLExtendedFetch**。 相反地，驅動程式管理員執行下列步驟時使用的 ODBC 2 *.x*驅動程式：  
  
1.  初始化內部的驅動程式管理員旗標*fSetPosError*為 TRUE。  
  
2.  當應用程式呼叫**SQLFetchScroll**，驅動程式管理員設定*fSetPosError*為 FALSE。  
  
3.  當應用程式呼叫**SQLSetStmtAttr**將 sql_attr_row_status_ptr 設定，來設定驅動程式管理員*fSetPosError* toTRUE 相等。  
  
4.  當應用程式呼叫**SQLSetPos**，與*fSetPosError*等於 TRUE，則驅動程式管理員會產生 sql_error，其中包含 SQLSTATE HY011 （屬性現在無法設定），表示應用程式嘗試呼叫**SQLSetPos**之後變更資料列狀態指標，但在呼叫前**SQLFetchScroll**。

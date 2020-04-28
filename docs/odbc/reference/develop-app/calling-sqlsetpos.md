---
title: 呼叫 SQLSetPos |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 46cfbb4e2e6b60f620cd7e38272bf9308ece91bc
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306239"
---
# <a name="calling-sqlsetpos"></a>呼叫 SQLSetPos
在 ODBC *2.x 中，* 資料列狀態陣列的指標是**SQLExtendedFetch**的引數。 資料列狀態陣列稍後會藉由呼叫**SQLSetPos**來進行更新。 有些驅動程式依賴此陣列在**SQLExtendedFetch**與**SQLSetPos**之間不會改變的事實。 在 ODBC 3.x 中，狀態陣列的指標是描述項*欄位，因此*應用程式可以輕鬆地將它變更為指向不同的陣列。 當 ODBC 3.x 應用程式*使用 odbc* 2.x*驅動程式，* 但呼叫**SQLSetStmtAttr**來設定陣列狀態指標，而且呼叫**SQLFetchScroll**來提取資料時，這可能會產生問題。 驅動程式管理員會將它對應為**SQLExtendedFetch**的一系列呼叫。 在下列程式碼中，通常會在驅動程式管理員對應第二個**SQLSetStmtAttr**呼叫（*使用 ODBC 2.x*驅動程式時）時引發錯誤：  
  
```  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, rgfRowStatus, 0);  
SQLFetchScroll(hstmt, fFetchType, iRow);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, rgfRowStat1, 0);  
SQLSetPos(hstmt, iRow, fOption, fLock);  
```  
  
 如果無法在**SQLExtendedFetch**的*呼叫之間變更*ODBC 2.x 中的資料列狀態指標，就會引發錯誤。 相反地，驅動程式管理員會在*使用 ODBC 2.x*驅動程式時執行下列步驟：  
  
1.  將內部驅動程式管理員旗標*fSetPosError*初始化為 TRUE。  
  
2.  當應用程式呼叫**SQLFetchScroll**時，驅動程式管理員會將*FSETPOSERROR*設定為 FALSE。  
  
3.  當應用程式呼叫**SQLSetStmtAttr**來設定 SQL_ATTR_ROW_STATUS_PTR 時，驅動程式管理員會將*fSetPosError*設定為相同的 toTRUE。  
  
4.  當應用程式呼叫**SQLSetPos**，並將*fSetPosError*等於 TRUE 時，驅動程式管理員會引發 SQL_ERROR 與 SQLSTATE HY011 （屬性無法立即設定），表示應用程式在變更資料列狀態指標之後，但在呼叫**SQLSetPos**之前，嘗試呼叫**SQLFetchScroll** 。

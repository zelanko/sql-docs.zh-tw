---
description: 呼叫 SQLSetPos
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
ms.openlocfilehash: ecb1708b6d5fe9877ab647b11488131645e56690
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494709"
---
# <a name="calling-sqlsetpos"></a>呼叫 SQLSetPos
在 ODBC *2.x 中，* 資料列狀態陣列的指標是要 **SQLExtendedFetch**的引數。 資料列狀態陣列稍後會透過呼叫 **SQLSetPos**進行更新。 有些驅動程式依賴此陣列不會在 **SQLExtendedFetch** 和 **SQLSetPos**之間變更的事實。 在 ODBC 3.x 中，狀態陣列的指標是描述項 *欄位，因此*應用程式可以輕鬆地將它變更為指向不同的陣列。 當 ODBC 3.x 應用程式正在*使用 odbc 2.x* *驅動程式，* 但正在呼叫**SQLSetStmtAttr**來設定陣列狀態指標，並且呼叫**SQLFetchScroll**來提取資料時，這可能會造成問題。 驅動程式管理員會將它對應為一系列的 **SQLExtendedFetch**呼叫。 在下列程式碼中，當*驅動程式管理員在使用 ODBC 2.x*驅動程式時對應第二個**SQLSetStmtAttr**呼叫時，通常會引發錯誤：  
  
```  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, rgfRowStatus, 0);  
SQLFetchScroll(hstmt, fFetchType, iRow);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, rgfRowStat1, 0);  
SQLSetPos(hstmt, iRow, fOption, fLock);  
```  
  
 如果無法在呼叫**SQLExtendedFetch***之間變更*ODBC 2.x 中的資料列狀態指標，就會引發錯誤。 相反地，驅動程式管理員會在 *使用 ODBC 2.x* 驅動程式時，執行下列步驟：  
  
1.  將內部驅動程式管理員旗標 *fSetPosError* 初始化為 TRUE。  
  
2.  當應用程式呼叫 **SQLFetchScroll**時，驅動程式管理員會將 *FSETPOSERROR* 設定為 FALSE。  
  
3.  當應用程式呼叫 **SQLSetStmtAttr** 來設定 SQL_ATTR_ROW_STATUS_PTR 時，驅動程式管理員會設定 *fSetPosError* 等於 toTRUE。  
  
4.  當應用程式呼叫**SQLSetPos**，而*fSetPosError*等於 TRUE 時，驅動程式管理員會引發 SQL_ERROR，且目前無法設定 SQLSTATE HY011 (屬性) 表示應用程式在變更資料列狀態指標之後，但在呼叫**SQLSetPos**之前，嘗試呼叫**SQLFetchScroll** 。

---
title: 呼叫 SQLSetPos |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306239"
---
# <a name="calling-sqlsetpos"></a>呼叫 SQLSetPos
在 ODBC *2.x*中,指向行狀態陣列的指標是**SQL 擴展獲取的**參數。 行狀態陣列後來被調用**SQLSetPos**更新。 某些驅動程式依賴於此陣列在**SQL 擴展獲取**和**SQLSetPos**之間不更改這一事實。 在 ODBC *3.x*中,指向狀態陣列的指標是一個描述符欄位,因此應用程式可以輕鬆地將其更改為指向其他陣列。 當 ODBC *3.x*應用程式使用 ODBC *2.x*驅動程式,但正在調用**SQLSetStmtAttr**來設置陣列狀態指標並調用**SQLFetchScroll**來獲取數據時,這可能是一個問題。 驅動程式管理員將其映射為對**SQL 延伸獲取**的呼叫序列。 在以下代碼中,當驅動程式管理器映射第二個**SQLSetStmtAttr**呼叫時,使用 ODBC *2.x*驅動程式時,通常會引發錯誤:  
  
```  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, rgfRowStatus, 0);  
SQLFetchScroll(hstmt, fFetchType, iRow);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, rgfRowStat1, 0);  
SQLSetPos(hstmt, iRow, fOption, fLock);  
```  
  
 如果無法在調用**SQLExtendedFetch**之間更改 ODBC *2.x*中的行狀態指標,則將引發該錯誤。 相反,驅動程式管理程式在使用 ODBC *2.x*驅動程式時執行以下步驟:  
  
1.  初始化內部驅動程式管理員標誌*fSetPosError*到 TRUE。  
  
2.  當應用程式呼叫**SQLFetchScroll**時,驅動程式管理員將*fSetPosError*設定為 FALSE。  
  
3.  當應用程式呼叫**SQLSetStmtAttr**設定為SQL_ATTR_ROW_STATUS_PTR時,驅動程式管理員將*fSetPosError*設定為等於 TRUE。  
  
4.  當應用程式呼叫**SQLSetPos**時 *,fSetPosError*等於 TRUE 時,驅動程式管理器會使用 SQLSTATE HY011(現在無法設置屬性)引發SQL_ERROR,以指示應用程式在更改行狀態指標後但在調用**SQLFetch**之前嘗試調用**SQLSetPos。**

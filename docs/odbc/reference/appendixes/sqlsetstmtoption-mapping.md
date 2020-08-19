---
description: SQLSetStmtOption 對應
title: SQLSetStmtOption 對應 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLSetStmtOption
- SQLSetStmtOption function [ODBC], mapping
ms.assetid: 6a9921aa-8a53-4668-9b13-87164062f1e5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f2c4a65ade202003d454988372895ba40fb6eeef
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424872"
---
# <a name="sqlsetstmtoption-mapping"></a>SQLSetStmtOption 對應
當應用程式*透過 ODBC 3.x 驅動程式呼叫* **SQLSetStmtOption**時，呼叫  
  
```  
SQLSetStmtOption(StatementHandle, fOption, vParam)  
```  
  
 將會產生如下的結果：  
  
-   如果 *fOption* 指出 ODBC 定義的語句屬性（字串），驅動程式管理員會呼叫  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, SQL_NTS)  
    ```  
  
-   如果 *fOption* 指出傳回32位整數值的 ODBC 定義語句屬性，驅動程式管理員會呼叫  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, 0)  
    ```  
  
-   如果 *fOption* 指出驅動程式定義的語句屬性，驅動程式管理員會呼叫  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, BufferLength)  
    ```  
  
 在上述三種情況下， **StatementHandle** 引數會設定為 *hstmt*中的值，而 *Attribute* 引數會設定為 *fOption*中的值，而 *ValuePtr* 引數會設為 *vParam*的值。  
  
 因為驅動程式管理員不知道驅動程式定義的語句屬性是否需要字串或32位整數值，所以必須針對**SQLSetStmtAttr**的*StringLength*引數傳入有效的值。 如果驅動程式已為驅動程式定義的語句屬性定義特殊的語法，且需要使用 **SQLSetStmtOption**來呼叫，則必須支援 **SQLSetStmtOption**。  
  
 如果應用程式在 ODBC 3.x 驅動程式中呼叫**SQLSetStmtOption**來設定驅動程式專屬的語句選項，且此選項定義于 odbc *2.x 版的**驅動程式中*，則應該*為 odbc 3.x*驅動程式中的選項定義新的資訊清單常數。 如果在 **SQLSetStmtOption**的呼叫中使用舊的資訊清單常數，驅動程式管理員會呼叫 **SQLSetStmtAttr** ，並將 *StringLength* 引數設定為0。  
  
 當應用程式呼叫 **SQLSetStmtAttr** 將 SQL_ATTR_USE_BOOKMARKS 設定 *為 ODBC 3.x* 驅動程式中的 SQL_UB_ON 時，SQL_ATTR_USE_BOOKMARKS 語句屬性會設定為 SQL_UB_FIXED。 SQL_UB_ON 與 SQL_UB_FIXED 的常數相同。 驅動程式管理員會將 SQL_UB_FIXED 傳遞至驅動程式。 ODBC 3.x 中的 SQL_UB_FIXED 已被取代，但是 ODBC *3.x 驅動程式*必須執行*它，才能*與使用固定長度書簽的 odbc *2.x 應用程式搭配使用。*  
  
 針對 ODBC 3.x 驅動程式， *驅動程式管理員* 不會再檢查 SQL_STMT_OPT_MIN 和 SQL_STMT_OPT_MAX 之間是否有 *選項* ，或大於 SQL_CONNECT_OPT_DRVR_START。

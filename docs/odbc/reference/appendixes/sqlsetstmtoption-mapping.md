---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dc4ed430b301f2b191c0586c0a54af19a2d2d526
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68091673"
---
# <a name="sqlsetstmtoption-mapping"></a>SQLSetStmtOption 對應
當應用程式*透過 ODBC 3.x 驅動程式呼叫* **SQLSetStmtOption**時，呼叫  
  
```  
SQLSetStmtOption(StatementHandle, fOption, vParam)  
```  
  
 將會產生如下所示：  
  
-   如果*fOption*表示 ODBC 定義的語句屬性為字串，驅動程式管理員會呼叫  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, SQL_NTS)  
    ```  
  
-   如果*fOption*表示 ODBC 定義的語句屬性，它會傳回32位的整數值，驅動程式管理員會呼叫  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, 0)  
    ```  
  
-   如果*fOption*表示驅動程式定義的語句屬性，驅動程式管理員會呼叫  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, BufferLength)  
    ```  
  
 在上述三種情況中， **StatementHandle**引數會設定為*hstmt*中的值，而*屬性*引數會設定為*fOption*中的值，而*Valueptr 是*引數會設定為值做為*vParam*。  
  
 因為驅動程式管理員不知道驅動程式定義的語句屬性是否需要字串或32位的整數值，所以必須針對**SQLSetStmtAttr**的*StringLength*引數傳入有效值。 如果驅動程式已針對驅動程式定義的語句屬性定義特殊的語義，而且需要使用**SQLSetStmtOption**來呼叫，則它必須支援**SQLSetStmtOption**。  
  
 如果應用程式呼叫**SQLSetStmtOption**在 odbc 3.x 驅動程式中設定驅動程式特定的語句選項，而且該選項是*在 odbc 2.x* *版本的*驅動程式中定義，則應該*針對 odbc 3.x*驅動程式中的選項定義新的資訊清單常數。 如果在呼叫**SQLSetStmtOption**時使用舊的資訊清單常數，驅動程式管理員將會呼叫**SQLSetStmtAttr** ，並將*StringLength*引數設定為0。  
  
 當應用程式呼叫**SQLSetStmtAttr** ，將 SQL_ATTR_USE_BOOKMARKS 設定*為 ODBC 3.x*驅動程式中的 SQL_UB_ON 時，SQL_ATTR_USE_BOOKMARKS 語句屬性會設定為 SQL_UB_FIXED。 SQL_UB_ON 與 SQL_UB_FIXED 的常數相同。 驅動程式管理員會將 SQL_UB_FIXED 傳遞至驅動程式。 SQL_UB_FIXED 在 ODBC 3.x 中已被*取代，但*odbc 3.x 驅動*程式*必須將它實作為搭配使用固定長度書簽的 odbc *2.x 應用*程式。  
  
 對於 ODBC 3.x 驅動程式，*驅動程式管理員*不會再檢查 SQL_STMT_OPT_MIN 和 SQL_STMT_OPT_MAX 之間是否有*選項*，或是大於 SQL_CONNECT_OPT_DRVR_START。

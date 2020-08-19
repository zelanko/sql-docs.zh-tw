---
description: SQLGetStmtOption 對應
title: SQLGetStmtOption 對應 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetStmtOption function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLGetStmtOption
ms.assetid: fa599517-3f3e-4dad-a65a-b8596ae3f330
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 01d099c4802c05f8e5bd1e093987f2c3993ac9c1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448978"
---
# <a name="sqlgetstmtoption-mapping"></a>SQLGetStmtOption 對應
當應用程式呼叫 **SQLGetStmtOption** 至不支援 *的 ODBC 3.x* 驅動程式時，呼叫  
  
```  
SQLGetStmtOption(hstmt, fOption, pvParam)  
```  
  
 將會產生如下的結果：  
  
-   如果 *fOption* 指出會傳回字串的 ODBC 定義語句選項，驅動程式管理員會呼叫  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
-   如果 *fOption* 指出傳回32位整數值的 ODBC 定義語句選項，驅動程式管理員會呼叫  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, 0, NULL)  
    ```  
  
-   如果 *fOption* 指出驅動程式定義的語句選項，驅動程式管理員會呼叫  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
 在上述三種情況下， *StatementHandle* 引數會設定為 *hstmt*中的值、 *屬性* 引數設定為 *fOption*中的值，而 *ValuePtr* 引數則設定為與 *pvParam*相同的值。  
  
 若為 ODBC 定義的字串連接選項，驅動程式管理員會將**SQLGetConnectAttr**呼叫中的*BufferLength*引數設定為預先定義的最大長度 (SQL_MAX_OPTION_STRING_LENGTH) ;若為非字串連接選項， *BufferLength*會設定為0。  
  
 ODBC 3.x 中的 SQL_GET_BOOKMARK 語句選項已被*取代。* 若要讓 ODBC 3.x 驅動程式處理使用 SQL_GET_BOOKMARK 的*odbc 2.x* *應用程式，* 它必須支援 SQL_GET_BOOKMARK。 若要讓 ODBC 3.x 驅動程式*使用 odbc 2.x* *應用程式，* 它必須支援將 SQL_USE_BOOKMARKS 設定為 SQL_UB_ON，而且應該公開固定長度的書簽。 如果 ODBC 3.x *驅動程式* 僅支援可變長度的書簽，而不支援固定長度的書簽，則如果 odbc 2.x *應用程式* 嘗試將 SQL_USE_BOOKMARKS 設定為 SQL_UB_ON，它必須傳回 SQLSTATE HYC00 (選用功能未實) 。  
  
 針對 ODBC 3.x 驅動程式， *驅動程式管理員* 不會再檢查 *選項* 是否介於 SQL_STMT_OPT_MIN 和 SQL_STMT_OPT_MAX 之間，或是大於 SQL_CONNECT_OPT_DRVR_START。 驅動程式必須核取此選項。

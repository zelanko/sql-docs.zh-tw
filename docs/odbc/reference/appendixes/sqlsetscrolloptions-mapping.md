---
title: SQLSetScrollOptions 對應 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLSetScrollOptions
ms.assetid: a0fa4510-8891-4a61-a867-b2555bc35f05
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 06b6b0f982b5c8d864e5024c8544f1f8e9af75ac
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68091700"
---
# <a name="sqlsetscrolloptions-mapping"></a>SQLSetScrollOptions 對應
當應用程式*透過 ODBC 3.x 驅動程式呼叫* **SQLSetScrollOptions** ，而驅動程式不支援**SQLSetScrollOptions**時，呼叫  
  
```  
SQLSetScrollOptions(StatementHandle, Concurrency, KeysetSize, RowsetSize)  
```  
  
 將會產生如下所示：  
  
-   呼叫  
  
    ```  
    SQLGetInfo(ConnectionHandle, InfoType, InfoValuePtr, BufferLength, StringLengthPtr)  
    ```  
  
     將*InfoType*引數設定為下表中的其中一個值，視**SQLSetScrollOptions**中的*KeysetSize*引數值而定。  
  
    |*KeysetSize 引數*|*InfoType 引數*|  
    |---------------------------|-------------------------|  
    |SQL_SCROLL_FORWARD_ONLY|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_STATIC|SQL_STATIC_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_KEYSET_DRIVEN|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_DYNAMIC|SQL_DYNAMIC_CURSOR_ATTRIBUTES2|  
    |大於*RowsetSize*引數的值|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
  
     如果*KeysetSize*引數的值未列在上表中，則對**SQLSetScrollOptions**的呼叫會傳回 SQLSTATE S1107 （資料列值超出範圍），而且不會執行下列任何步驟。  
  
     然後，驅動程式管理員會根據**SQLSetScrollOptions**中的*Concurrency*引數值，驗證是否已在**SQLGetInfo**的呼叫所傳回的 **InfoValuePtr*值中設定適當的位。  
  
    |*Concurrency*引數|*InfoType*設定|  
    |----------------------------|------------------------|  
    |SQL_CONCUR_READ_ONLY|SQL_CA2_READ_ONLY_CONCURRENCY|  
    |SQL_CONCUR_LOCK|SQL_CA2_LOCK_CONCURRENCY|  
    |SQL_CONCUR_ROWVER|SQL_CA2_ROWVER_CONCURRENCY|  
    |SQL_CONCUR_VALUES|SQL_CA2_VALUES_CONCURRENCY|  
  
     如果*Concurrency*引數不是上表中的其中一個值，則對**SQLSetScrollOptions**的呼叫會傳回 SQLSTATE S1108 （並行選項超出範圍），而且不會執行下列任何步驟。 如果將適當的位（如上表所示）未*設定為對應至**並行*引數的其中一個值，則對**SQLSETSCROLLOPTIONS**的呼叫會傳回 SQLSTATE S1C00 （驅動程式不支援），而且不會執行下列任何步驟。  
  
-   呼叫  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_CURSOR_TYPE, ValuePtr, 0)  
    ```  
  
     根據**SQLSetScrollOptions**中的*KeysetSize*引數值，將* \*valueptr 是*設定為下表中的其中一個值。  
  
    |*KeysetSize*引數|*\*Valueptr 是*|  
    |---------------------------|------------------|  
    |SQL_SCROLL_FORWARD_ONLY|SQL_CURSOR_FORWARD_ONLY|  
    |SQL_SCROLL_STATIC|SQL_CURSOR_STATIC|  
    |SQL_SCROLL_KEYSET_DRIVEN|SQL_CURSOR_KEYSET_DRIVEN|  
    |SQL_SCROLL_DYNAMIC|SQL_CURSOR_DYNAMIC|  
    |大於*RowsetSize*引數的值|SQL_CURSOR_KEYSET_DRIVEN|  
  
-   呼叫  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_CONCURRENCY, ValuePtr, 0)  
    ```  
  
     當* \*valueptr 是*設定為**SQLSetScrollOptions**中的*Concurrency*引數時。  
  
-   如果**SQLSetScrollOptions**呼叫中的*KeysetSize*引數是正數，則呼叫  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_KEYSET_SIZE, ValuePtr, 0)  
    ```  
  
     將* \*valueptr 是*設定為**SQLSetScrollOptions**中的*KeysetSize*引數。  
  
-   呼叫  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ROWSET_SIZE, ValuePtr, 0)  
    ```  
  
     將* \*valueptr 是*設定為**SQLSetScrollOptions**中的*RowsetSize*引數。  
  
    > [!NOTE]  
    >  當驅動程式管理員對應的應用程式使用不支援**SQLSetScrollOptions**的*ODBC 3.X 驅動程式* **SQLSetScrollOptions**時，驅動程式管理員會將 SQL_ROWSET_SIZE 語句選項（而非 SQL_ATTR_ROW_ARRAY_SIZE 語句屬性）設定為**SQLSetScrollOption**中的*RowsetSize*引數。 因此，在透過呼叫**SQLFetch**或**SQLFetchScroll**來提取多個資料列時，應用程式無法使用**SQLSetScrollOptions** 。 只有在透過呼叫**SQLExtendedFetch**來提取多個資料列時，才能使用此方法。

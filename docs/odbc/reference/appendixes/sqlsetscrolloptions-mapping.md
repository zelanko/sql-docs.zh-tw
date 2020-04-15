---
title: SQLSetScroll 選項映射 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 77050df283b10abd17ba62a48bd366d6c1b3f601
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300498"
---
# <a name="sqlsetscrolloptions-mapping"></a>SQLSetScrollOptions 對應
當應用程式透過 ODBC *3.x*驅動程式呼叫**SQLSetScrollOptions,** 並且驅動程式不支援**SQLSetScrollOptions**時,呼叫  
  
```  
SQLSetScrollOptions(StatementHandle, Concurrency, KeysetSize, RowsetSize)  
```  
  
 結果如下:  
  
-   通話  
  
    ```  
    SQLGetInfo(ConnectionHandle, InfoType, InfoValuePtr, BufferLength, StringLengthPtr)  
    ```  
  
     InfoType*InfoType*參數設定為下表中的一個值,具體取決於**SQLSetScrollOptions**中的*KeysetSize*參數的值。  
  
    |*鍵集大小參數*|*資訊類型參數*|  
    |---------------------------|-------------------------|  
    |SQL_SCROLL_FORWARD_ONLY|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_STATIC|SQL_STATIC_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_KEYSET_DRIVEN|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_DYNAMIC|SQL_DYNAMIC_CURSOR_ATTRIBUTES2|  
    |大於*RowsetSize*參數的值|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
  
     如果上表中未列出*KeysetSize*參數的值,則對**SQLSetScrollOptions 的**呼叫將返回 SQLSTATE S1107(行值不在範圍範圍內),並且不執行以下步驟。  
  
     然後,驅動程式管理器根據**SQLSetScrollOptions***中 併發*參數的值,驗證是否在調用**SQLGetInfo**傳回的 #*InfoValuePtr*值中設定了適當的位。  
  
    |*併發*參數|*資訊類型*設定|  
    |----------------------------|------------------------|  
    |SQL_CONCUR_READ_ONLY|SQL_CA2_READ_ONLY_CONCURRENCY|  
    |SQL_CONCUR_LOCK|SQL_CA2_LOCK_CONCURRENCY|  
    |SQL_CONCUR_ROWVER|SQL_CA2_ROWVER_CONCURRENCY|  
    |SQL_CONCUR_VALUES|SQL_CA2_VALUES_CONCURRENCY|  
  
     如果*併發*參數不是上表中的值之一,則對**SQLSetScrollOption 的**調用將返回 SQLSTATE S1108(在範圍外不變選項),並且不執行以下步驟。 如果未在 #*InfoValuePtr*中設定相應的位(如上表所示),則對**SQLSetScrollOptions**的*Concurrency*呼叫將傳回 SQLSTATE S1C00(驅動程式無法執行),並且不執行以下步驟。  
  
-   通話  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_CURSOR_TYPE, ValuePtr, 0)  
    ```  
  
     根據**SQLSetScrollOptions**中的*KeysetSize*參數的值*\*,ValuePtr*設置為下表中的一個值。  
  
    |*鍵集大小*參數|*\*價值Ptr*|  
    |---------------------------|------------------|  
    |SQL_SCROLL_FORWARD_ONLY|SQL_CURSOR_FORWARD_ONLY|  
    |SQL_SCROLL_STATIC|SQL_CURSOR_STATIC|  
    |SQL_SCROLL_KEYSET_DRIVEN|SQL_CURSOR_KEYSET_DRIVEN|  
    |SQL_SCROLL_DYNAMIC|SQL_CURSOR_DYNAMIC|  
    |大於*RowsetSize*參數的值|SQL_CURSOR_KEYSET_DRIVEN|  
  
-   通話  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_CONCURRENCY, ValuePtr, 0)  
    ```  
  
     將*\*ValuePtr*設定為**SQLSetScrollOptions**中的*併發*參數。  
  
-   如果對**SQLSetScrollOptions**的呼叫中的*KeysetSize*參數為正參數,則呼叫  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_KEYSET_SIZE, ValuePtr, 0)  
    ```  
  
     將*\*ValuePtr*設定為**SQLSetScroll 選項**中的*KeysetSize*參數。  
  
-   通話  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ROWSET_SIZE, ValuePtr, 0)  
    ```  
  
     將*\*ValuePtr*設定為**SQLSetScroll 選項**中的*RowsetSize*參數。  
  
    > [!NOTE]  
    >  當驅動程式管理器對應**SQLSetScrollOption 的應用程式 SQLSetScrollOption**時,使用不支援**SQLSetScrollOption**的 ODBC *3.x*驅動程式時,驅動程式管理器將SQL_ROWSET_SIZE語句選項(而不是SQL_ATTR_ROW_ARRAY_SIZE語句屬性)設置為**SQLSetScrollOption**中的*RowsetSize*參數。 因此,當調用**SQLFetch**或**SQLFetchScroll**獲取多行時,應用程式無法使用**SQLSetScrollOptions。** 它只能在調用**SQLExtendedFetch**獲取多行時使用。

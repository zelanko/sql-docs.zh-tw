---
title: SQLSetConnectAttr （資料指標程式庫） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectAttr function [ODBC], Cursor Library
ms.assetid: 6f70bbd0-a057-49ef-8b05-4c80b58fc6e6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a87c85d727fb9eb2fc27613b9eecd3fe0ec51b58
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300538"
---
# <a name="sqlsetconnectattr-cursor-library"></a>SQLSetConnectAttr (資料指標程式庫)
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論如何在資料指標程式庫中使用**SQLSetConnectAttr**函數。 如需有關**SQLSetConnectAttr**的一般資訊，請參閱[SQLSetConnectAttr 函數](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)。  
  
 應用程式會使用 SQL_ATTR_ODBC_CURSORS 屬性來呼叫**SQLSetConnectAttr** ，以指定是否一律使用資料指標程式庫（如果驅動程式不支援可滾動的資料指標，或從未使用過）。 資料指標程式庫假設如果驅動程式在**SQLGetInfo**中傳回 SQL_STATIC_CURSOR_ATTRIBUTES1 資訊類型的 SQL_CA1_RELATIVE，就會支援可滾動的資料指標。  
  
 應用程式必須呼叫**SQLSetConnectAttr**來指定資料指標程式庫的使用方式，它會在呼叫具有*HandleType* SQL_HANDLE_DBC 的**SQLAllocHandle**之後，才會配置連接，然後再連接到資料來源。 如果應用程式在連接仍在使用中時，以 SQL_ATTR_ODBC_CURSORS 屬性呼叫**SQLSetConnectAttr** ，則資料指標程式庫會傳回錯誤。  
  
 若要針對與連接相關聯的所有語句，設定資料指標程式庫所支援的語句屬性，應用程式必須在連接到資料來源之後，以及在開啟游標之前，呼叫該語句屬性的**SQLSetConnectAttr** 。 如果應用程式使用語句屬性呼叫**SQLSetConnectAttr** ，而且在與連接相關聯的語句上開啟資料指標，則語句屬性將不會套用至該語句，直到資料指標關閉並重新開啟為止。

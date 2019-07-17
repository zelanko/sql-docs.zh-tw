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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 73d1369a2bce0327ac3367d33f0894bdcfab8205
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125575"
---
# <a name="sqlsetconnectattr-cursor-library"></a>SQLSetConnectAttr (資料指標程式庫)
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論使用**SQLSetConnectAttr**資料指標程式庫中的函式。 如需一般資訊**SQLSetConnectAttr**，請參閱[SQLSetConnectAttr 函數](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)。  
  
 應用程式呼叫**SQLSetConnectAttr**與指定資料指標程式庫是一律使用、 使用驅動程式不支援可捲動資料指標，或從未使用過之 SQL_ATTR_ODBC_CURSORS 屬性。 資料指標程式庫假設驅動程式支援可捲動資料指標，如果它傳回 SQL_STATIC_CURSOR_ATTRIBUTES1 類型資訊，請在 SQL_CA1_RELATIVE **SQLGetInfo**。  
  
 應用程式必須呼叫**SQLSetConnectAttr**若要指定資料指標程式庫使用方式之後它會呼叫, **SQLAllocHandle**具有*HandleType*配置利用 SQL_HANDLE_DBC 的連線和才能連線到資料來源。 如果應用程式呼叫**SQLSetConnectAttr**之 SQL_ATTR_ODBC_CURSORS 屬性仍在作用中，連接時資料指標程式庫會傳回錯誤。  
  
 若要設定與連接相關聯的所有陳述式的資料指標程式庫所支援的陳述式屬性，應用程式必須呼叫**SQLSetConnectAttr**連線資料來源並在它之前後，該陳述式屬性開啟資料指標。 如果應用程式呼叫**SQLSetConnectAttr**陳述式屬性和資料指標開啟時與連接相關聯的陳述式，陳述式屬性將不會套用至該陳述式之前關閉資料指標和重新開啟。

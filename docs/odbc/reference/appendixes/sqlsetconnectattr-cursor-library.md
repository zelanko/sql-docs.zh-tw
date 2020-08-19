---
description: SQLSetConnectAttr (資料指標程式庫)
title: SQLSetConnectAttr (資料指標程式庫) |Microsoft Docs
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
ms.openlocfilehash: 3b809ad81e9edaca7fbe7d40952673a1698f113e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424890"
---
# <a name="sqlsetconnectattr-cursor-library"></a>SQLSetConnectAttr (資料指標程式庫)
> [!IMPORTANT]  
>  未來的 Windows 版本將會移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論如何在資料指標程式庫中使用 **SQLSetConnectAttr** 函數。 如需 **SQLSetConnectAttr**的一般資訊，請參閱 [SQLSetConnectAttr 函數](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)。  
  
 應用程式會使用 SQL_ATTR_ODBC_CURSORS 屬性來呼叫 **SQLSetConnectAttr** ，以指定是否一律使用資料指標程式庫，如果驅動程式不支援可滾動的資料指標或從未使用，則會使用此資料指標程式庫。 如果驅動程式在 **SQLGetInfo**中傳回 SQL_STATIC_CURSOR_ATTRIBUTES1 資訊類型 SQL_CA1_RELATIVE，則會假設驅動程式支援可滾動的資料指標。  
  
 應用程式必須呼叫**SQLSetConnectAttr**來指定資料指標程式庫使用方式，然後再呼叫具有 SQL_HANDLE_DBC *HandleType*的**SQLAllocHandle** ，以配置連接並連接到資料來源。 如果應用程式在連接仍在使用中時使用 SQL_ATTR_ODBC_CURSORS 屬性來呼叫 **SQLSetConnectAttr** ，則資料指標程式庫會傳回錯誤。  
  
 若要為與連接相關聯的所有語句設定資料指標程式庫所支援的語句屬性，應用程式必須在連接到資料來源之後，以及開啟資料指標之前，呼叫該語句屬性的 **SQLSetConnectAttr** 。 如果應用程式使用語句屬性來呼叫 **SQLSetConnectAttr** ，並在與該連接相關聯的語句上開啟資料指標，則在關閉並重新開啟資料指標之前，語句屬性不會套用到該語句。

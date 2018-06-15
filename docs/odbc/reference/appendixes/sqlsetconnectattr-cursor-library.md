---
title: SQLSetConnectAttr （資料指標程式庫） |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectAttr function [ODBC], Cursor Library
ms.assetid: 6f70bbd0-a057-49ef-8b05-4c80b58fc6e6
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d10356488b0a590fb065c49a36a05f0e9b976991
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32907703"
---
# <a name="sqlsetconnectattr-cursor-library"></a>SQLSetConnectAttr （資料指標程式庫）
> [!IMPORTANT]  
>  將移除這項功能，在未來的版本的 Windows。 避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論使用**SQLSetConnectAttr**資料指標程式庫中的函式。 如需一般資訊**SQLSetConnectAttr**，請參閱[SQLSetConnectAttr 函數](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)。  
  
 應用程式呼叫**SQLSetConnectAttr** SQL_ATTR_ODBC_CURSORS 屬性來指定資料指標程式庫會一律使用、 驅動程式不支援可捲動資料指標，如果使用或從未使用過。 資料指標程式庫假設驅動程式支援可捲動資料指標，如果它傳回 SQL_CA1_RELATIVE SQL_STATIC_CURSOR_ATTRIBUTES1 類型資訊，請在**SQLGetInfo**。  
  
 應用程式必須呼叫**SQLSetConnectAttr**之後，它會呼叫指定的資料指標程式庫使用量**SQLAllocHandle**與*HandleType*配置利用 SQL_HANDLE_DBC 的連接和才能連線到資料來源。 如果應用程式呼叫**SQLSetConnectAttr** SQL_ATTR_ODBC_CURSORS 屬性連接時仍在作用中，資料指標程式庫會傳回錯誤。  
  
 若要設定與連接相關聯的所有陳述式的資料指標程式庫所支援的陳述式屬性，應用程式必須呼叫**SQLSetConnectAttr**連線至資料來源，以及之前後，該陳述式屬性開啟資料指標。 如果應用程式呼叫**SQLSetConnectAttr**與陳述式屬性和資料指標開啟時與連接相關聯的陳述式，陳述式屬性將不會套用到該陳述式直到關閉資料指標和重新開啟。

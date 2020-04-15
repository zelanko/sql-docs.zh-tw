---
title: 動態跟蹤 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- tracing options [ODBC], dynamic
- dynamic tracing [ODBC]
ms.assetid: ebe58a83-a7b0-4747-86c8-2af2940471ef
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8cbd2dbae4f4b437f45845ce2791f4a9b0aa8c8b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305762"
---
# <a name="dynamic-tracing"></a>動態追蹤
可以在應用程式運行的任何點啟用或禁用跟蹤。 這允許應用程式跟蹤任意數量的函數調用。  
  
 變數**ODBCSharedTraceFlag**設置為動態啟用跟蹤。 此變數在驅動程式管理器的所有正在運行的副本之間共用。 如果任何應用程式設定此變數,則為當前運行的所有 ODBC 應用程式啟用追蹤。 要在啟用動態追蹤時關閉跟蹤,應用程式將調用**SQLSetConnect Attr**以將SQL_ATTR_TRACE設置為SQL_TRACE_OFF。 此調用將僅關閉該應用程式的跟蹤。 與 Odbc32.lib 連結的應用程式可以修改此變數的使用。 追蹤資料可以顯示在即時視窗中,而不是追蹤檔案,必須在 ODBC 作業階段後打開。 可以將控制項添加到應用程式的螢幕以打開或關閉追蹤。  
  
 ODBC 3 *.x*附帶的跟蹤 DLL 不具有線程安全。 如果啟用了全域跟蹤(設置了變數**ODBCSharedTraceFlag),** 並且多個應用程式同時寫入跟蹤檔,則不能保證日誌檔的寫入正確。 此條件不會返回錯誤。

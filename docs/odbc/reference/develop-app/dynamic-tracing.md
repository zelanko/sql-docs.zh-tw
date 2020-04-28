---
title: 動態追蹤 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305762"
---
# <a name="dynamic-tracing"></a>動態追蹤
在應用程式執行中的任何時間點，都可以啟用或停用追蹤。 這可讓應用程式追蹤任何數目的函式呼叫。  
  
 變數**ODBCSharedTraceFlag**設定為動態啟用追蹤。 此變數會在驅動程式管理員的所有執行中複本之間共用。 如果有任何應用程式設定此變數，則會針對目前正在執行的所有 ODBC 應用程式啟用追蹤。 若要在啟用動態追蹤時關閉追蹤功能，應用程式會呼叫**SQLSetConnectAttr** ，將 SQL_ATTR_TRACE 設定為 SQL_TRACE_OFF。 此呼叫只會針對該應用程式關閉追蹤。 與 Odbc32.lib 連結的應用程式可以修改這個變數的使用。 追蹤資料可以顯示在即時視窗中，而不是追蹤檔案（必須在 ODBC 會話之後開啟）。 控制項可以新增至應用程式的畫面，以開啟或關閉追蹤。  
  
 ODBC 3.x 隨附的追蹤 DLL 不*是安全*執行緒。 如果已啟用全域追蹤（已設定變數**ODBCSharedTraceFlag** ），而且有一個以上的應用程式同時寫入追蹤檔案，則不保證記錄檔的寫入正確。 此狀況不會傳回錯誤。

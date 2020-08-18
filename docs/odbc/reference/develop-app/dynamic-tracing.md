---
description: 動態追蹤
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
ms.openlocfilehash: a1618d1b2837c5169f03b07900aba3921bc98659
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482991"
---
# <a name="dynamic-tracing"></a>動態追蹤
您可以在應用程式執行中的任何時間點，啟用或停用追蹤。 這可讓應用程式追蹤任意數目的函式呼叫。  
  
 變數 **ODBCSharedTraceFlag** 設定為動態啟用追蹤。 此變數會在驅動程式管理員的所有執行複本之間共用。 如果有任何應用程式設定此變數，則會針對目前正在執行的所有 ODBC 應用程式啟用追蹤。 若要在啟用動態追蹤時關閉追蹤功能，應用程式會呼叫 **SQLSetConnectAttr** ，將 SQL_ATTR_TRACE 設定為 SQL_TRACE_OFF。 此呼叫只會關閉該應用程式的追蹤。 連結到 Odbc32.lib 的應用程式可以修改這個變數的使用方式。 追蹤資料可以在即時視窗中顯示，而不是在必須于 ODBC 會話之後開啟的追蹤檔案中顯示。 您可以將控制項加入至應用程式的畫面，以開啟或關閉追蹤功能。  
  
 ODBC 3.x 隨附的追蹤 DLL 不*是安全* 執行緒。 如果已啟用全域追蹤 (變數 **ODBCSharedTraceFlag** 已設定) ，而且有一個以上的應用程式同時寫入至追蹤檔案，則不保證記錄檔的寫入正確。 這種情況不會傳回錯誤。

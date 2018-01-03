---
title: "動態追蹤 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- tracing options [ODBC], dynamic
- dynamic tracing [ODBC]
ms.assetid: ebe58a83-a7b0-4747-86c8-2af2940471ef
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 51ea74b8b54bf9d9e26bedf2733147e8552ce08f
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="dynamic-tracing"></a>動態追蹤
您可以啟用或停用在任何時間點執行的應用程式中追蹤。 這可讓應用程式以追蹤任何數目的函式呼叫。  
  
 變數**ODBCSharedTraceFlag**設為啟用動態追蹤。 此變數是所有執行中複本的驅動程式管理員之間共用的。 如果任何應用程式會將這個變數，所有目前正在執行的 ODBC 應用程式啟用追蹤。 若要開啟關閉時動態追蹤已啟用追蹤，應用程式呼叫**SQLSetConnectAttr** SQL_ATTR_TRACE 設 SQL_TRACE_OFF。 此呼叫將會開啟該應用程式只關閉追蹤。 使用 odbc32.lib 編譯連結的應用程式可以修改使用此變數。 追蹤資料可以顯示在即時的視窗中，而不是 ODBC 工作階段之後，必須開啟追蹤檔案。 控制項可以加入至開啟的應用程式的螢幕會在追蹤開啟或關閉。  
  
 追蹤 DLL 隨附 ODBC 3*.x*不是執行緒安全。 不保證如果已啟用全域追蹤記錄檔已正確寫入 (變數**ODBCSharedTraceFlag**設定)，並同時多個應用程式將寫入追蹤檔。 此條件不會傳回錯誤。

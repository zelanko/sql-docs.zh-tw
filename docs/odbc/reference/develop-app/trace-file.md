---
description: 追蹤檔案
title: 追蹤檔案 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- trace files [ODBC]
- tracing options [ODBC], trace files
ms.assetid: ec97f949-126f-40a2-b67e-e74520a524cb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ba45e44baaba68d1c203e83a25c9db305642e6d2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487491"
---
# <a name="trace-file"></a>追蹤檔案
應用程式會藉由在 Odbc.ini 登錄專案中設定 **TraceFile** 關鍵字，或透過 SQL_ATTR_TRACEFILE 連接屬性來呼叫 **SQLSetConnectAttr** ，來指定追蹤檔。 如果在啟用追蹤時檔案不存在，驅動程式管理員會建立檔案。 每個應用程式都應該有自己專用的追蹤檔案，以避免發生競爭情況。 應用程式可以使用一個以上的追蹤檔案;應用程式的安裝程式可以提供使用者選擇的追蹤檔案。 如果動態啟用追蹤，應用程式也可以顯示追蹤結果，而不是記錄到追蹤檔。  
  
 追蹤檔案會以所有引數的資料類型和值，提供每個 ODBC 函式呼叫的記錄。 它會記錄所有輸入函式，並使用傳回碼和錯誤狀態來記錄所有傳回的函式。  
  
 在 ODBC *3.x 中，* 不會將連接函數的參數提供給追蹤 DLL。

---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c94c3718c116b37eb198264887dfb4a319bd1dc3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67985146"
---
# <a name="trace-file"></a>追蹤檔案
應用程式指定的追蹤檔藉由設定**TraceFile**關鍵字在 Odbc.ini 的登錄項目，或藉由呼叫**SQLSetConnectAttr** SQL_ATTR_TRACEFILE 連接屬性。 如果檔案不存在，當啟用追蹤時，驅動程式管理員會建立檔案。 每個應用程式應該有自己專用的追蹤檔案，以避免爭用。 應用程式可以使用一個以上的追蹤檔案;為使用者選擇一種追蹤檔案時，可以提供應用程式的安裝程式。 如果以動態方式啟用追蹤，應用程式也可以顯示追蹤結果，而不是記錄至追蹤檔案。  
  
 追蹤檔案提供的資料類型的每個 ODBC 函式呼叫的記錄檔和所有的引數的值。 它會記錄所有輸入的函式，並使用傳回碼和錯誤狀態來記錄所有傳回的函式。  
  
 在 ODBC *3.x*，連線函式參數不會提供追蹤 DLL。

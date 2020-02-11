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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67985146"
---
# <a name="trace-file"></a>追蹤檔案
應用程式會指定追蹤檔案，方法是在 Odbc .ini 登錄專案中設定**TraceFile**關鍵字，或使用 SQL_ATTR_TRACEFILE 連接屬性呼叫**SQLSetConnectAttr** 。 當啟用追蹤時，如果檔案不存在，驅動程式管理員會建立檔案。 每個應用程式都應該有自己的專用追蹤檔案，以避免發生爭用。 應用程式可以使用一個以上的追蹤檔案;應用程式的安裝程式可以為使用者提供追蹤檔案的選擇。 如果動態啟用追蹤，應用程式也可以顯示追蹤結果，而不是記錄到追蹤檔案。  
  
 追蹤檔案會使用所有引數的資料類型和值，提供每個 ODBC 函式呼叫的記錄檔。 它會記錄所有的輸入函式，並以傳回碼和錯誤狀態記錄所有傳回的函式。  
  
 在 ODBC *3.x 中，* 連接函數的參數不會提供給追蹤 DLL。

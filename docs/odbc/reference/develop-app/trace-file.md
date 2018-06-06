---
title: 追蹤檔案 |Microsoft 文件
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
- trace files [ODBC]
- tracing options [ODBC], trace files
ms.assetid: ec97f949-126f-40a2-b67e-e74520a524cb
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: eb9089ed49e623247384557e8650731f6abc9816
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="trace-file"></a>追蹤檔案
應用程式指定追蹤檔所設定的其中一種**TraceFile**關鍵字在 Odbc.ini 的登錄項目，或藉由呼叫**SQLSetConnectAttr** SQL_ATTR_TRACEFILE 連接屬性。 如果檔案不存在，當啟用追蹤時，驅動程式管理員會建立檔案。 每個應用程式應該有自己專用的追蹤檔案，以避免競爭。 應用程式可以使用多個追蹤檔案;追蹤檔案的各種使用者時，可以提供應用程式的安裝程式。 如果以動態方式啟用追蹤，應用程式也可以顯示追蹤結果，而不是記錄至追蹤檔案。  
  
 追蹤檔案提供的資料類型的每個 ODBC 函數呼叫的記錄檔和所有引數的值。 它會記錄所有輸入函式，並使用傳回碼和錯誤狀態來記錄所有傳回的函式。  
  
 在 ODBC 3 *.x*，來追蹤 DLL 未提供連線函式的參數。

---
title: 追蹤檔案 |微軟文件
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
ms.openlocfilehash: ddd0ee24649592cf4a1a296a51404334145a3bab
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298055"
---
# <a name="trace-file"></a>追蹤檔案
應用程式通過在 Odbc.ini 註冊表條目中設置**TraceFile**關鍵字或使用SQL_ATTR_TRACEFILE連接屬性調用**SQLSetConnectAttr**來指定追蹤檔。 如果啟用追蹤時檔案不存在,驅動程式管理員將創建該檔。 每個應用程式都應有自己的專用跟蹤檔,以避免爭用。 應用程式可以使用多個追蹤檔;但是,應用程式可以使用多個跟蹤檔。應用程式的安裝程式可以為使用者提供跟蹤檔的選擇。 如果動態啟用了跟蹤,則應用程式還可以顯示跟蹤結果,而不是登錄到跟蹤檔。  
  
 跟蹤檔提供每個 ODBC 函數調用的紀錄,包含所有參數的資料類型和值。 它記錄所有輸入函數,並記錄所有返回的函數,並帶有返回代碼和錯誤狀態。  
  
 在 ODBC *3.x*中,連接函數的參數不提供給跟蹤 DLL。

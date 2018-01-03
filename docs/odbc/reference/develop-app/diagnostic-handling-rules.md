---
title: "診斷處理規則 |Microsoft 文件"
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
- diagnostic information [ODBC], SqlGetDiagField
- SQLGetDiagField function [ODBC], diagnostic handling rules
- SQLGetDiagRec function [ODBC], diagnostic handling rules
- diagnostic information [ODBC], SqlGetDiagRec
ms.assetid: 74387c3a-d6b3-4c35-b209-b9612602b20a
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d7dde3b01f27efb992640594d46756b38cb94ede
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="diagnostic-handling-rules"></a>診斷的處理規則
下列規則可控制中的診斷處理**SQLGetDiagRec**和**SQLGetDiagField**。  
  
 所有的 ODBC 元件：  
  
-   必須不取代、 更改或遮罩錯誤或警告收到來自另一個 ODBC 元件。  
  
-   從另一個 ODBC 元件收到診斷訊息時，可能會新增額外的狀態記錄。 加入一筆記錄都必須將實際資訊值加入原始訊息。  
  
 Odbc 元件直接介面的資料來源：  
  
-   廠商識別碼、 其元件識別碼和診斷訊息在收到資料來源的資料來源的識別項必須前置詞。  
  
-   必須保留資料來源的原生錯誤碼。  
  
-   必須保留資料來源的診斷訊息。  
  
 會產生錯誤或警告不受影響資料來源的任何 ODBC 元件：  
  
-   必須提供正確的 SQLSTATE 的錯誤或警告。  
  
-   必須先產生診斷訊息的文字。  
  
-   必須在前面的廠商識別項和診斷訊息及其元件識別碼。  
  
-   如果其中一個可用且有意義，則必須傳回原生錯誤碼。  
  
 ODBC 元件之介面的驅動程式管理員：  
  
-   必須初始化的輸出引數**SQLGetDiagRec**和**SQLGetDiagField**。  
  
-   必須格式化，並傳回診斷資訊的輸出引數為**SQLGetDiagRec**和**SQLGetDiagField**呼叫該函式時。  
  
 一個 ODBC 元件以外，驅動程式管理員：  
  
-   必須設定根據原生錯誤的 SQLSTATE。 以檔案為基礎的驅動程式和 DBMS 架構驅動程式不使用閘道，驅動程式必須設定 SQLSTATE。 DBMS 架構驅動程式所使用的閘道，驅動程式或支援 ODBC 的閘道可能設定 SQLSTATE。

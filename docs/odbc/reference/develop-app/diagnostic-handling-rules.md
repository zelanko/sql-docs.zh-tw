---
title: 診斷處理規則 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], SqlGetDiagField
- SQLGetDiagField function [ODBC], diagnostic handling rules
- SQLGetDiagRec function [ODBC], diagnostic handling rules
- diagnostic information [ODBC], SqlGetDiagRec
ms.assetid: 74387c3a-d6b3-4c35-b209-b9612602b20a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 269e021d3fd4610c2fccda46bcd8ca160982543c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039923"
---
# <a name="diagnostic-handling-rules"></a>診斷處理規則
下列規則可管理中的診斷處理**SQLGetDiagRec**並**SQLGetDiagField**。  
  
 所有的 ODBC 元件：  
  
-   必須不取代、 更改或遮罩錯誤或警告收到來自另一個 ODBC 元件。  
  
-   從另一個 ODBC 元件收到診斷訊息時，可以新增的額外狀態記錄。 加入一筆記錄都必須將實際的資訊值加入原始訊息。  
  
 Odbc 元件直接介面的資料來源：  
  
-   廠商識別碼、 其元件識別碼，以及要接收從資料來源的診斷訊息的資料來源的識別項必須前置詞。  
  
-   必須保留資料來源的原生錯誤碼。  
  
-   必須保留資料來源的診斷訊息。  
  
 任何會產生錯誤或警告無關的資料來源的 ODBC 元件：  
  
-   必須提供正確的錯誤或警告的 SQLSTATE。  
  
-   必須產生診斷訊息的文字。  
  
-   必須在前面其廠商的識別項和其元件識別碼的診斷訊息。  
  
-   如果有可用且有意義時，就必須傳回原生錯誤碼。  
  
 ODBC 元件的介面與驅動程式管理員：  
  
-   必須初始化的輸出引數**SQLGetDiagRec**並**SQLGetDiagField**。  
  
-   必須設定的格式，並傳回輸出引數形式的診斷資訊**SQLGetDiagRec**並**SQLGetDiagField**時呼叫該函式。  
  
 一個 ODBC 元件以外，驅動程式管理員：  
  
-   必須設定根據原生錯誤的 SQLSTATE。 如需檔案為基礎的驅動程式和以 DBMS 為基礎的驅動程式，不會使用閘道，驅動程式必須設定 SQLSTATE。 以 DBMS 為基礎的驅動程式所使用的閘道，驅動程式或支援 ODBC 的閘道可能會設定 SQLSTATE。

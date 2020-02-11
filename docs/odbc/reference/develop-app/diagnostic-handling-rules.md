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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68039923"
---
# <a name="diagnostic-handling-rules"></a>診斷處理規則
下列規則會管理**SQLGetDiagRec**和**SQLGetDiagField**中的診斷處理。  
  
 針對所有 ODBC 元件：  
  
-   不得取代、改變或遮罩從另一個 ODBC 元件收到的錯誤或警告。  
  
-   可能會在收到來自另一個 ODBC 元件的診斷訊息時，加入額外的狀態記錄。 新增的記錄必須將實際的資訊值新增至原始訊息。  
  
 針對直接介面資料來源的 ODBC 元件：  
  
-   必須將其廠商識別碼、元件識別碼，以及資料來源識別碼的前置詞加到它從資料來源接收的診斷訊息。  
  
-   必須保留資料來源的原生錯誤碼。  
  
-   必須保留資料來源的診斷訊息。  
  
 針對產生與資料來源無關之錯誤或警告的任何 ODBC 元件：  
  
-   必須提供錯誤或警告的正確 SQLSTATE。  
  
-   必須產生診斷訊息的文字。  
  
-   必須在診斷訊息中加上其廠商識別碼及其元件識別碼的前置詞。  
  
-   必須傳回原生錯誤碼（如果有的話），以及有意義的錯誤碼。  
  
 針對與驅動程式管理員介面的 ODBC 元件：  
  
-   必須初始化**SQLGetDiagRec**和**SQLGetDiagField**的輸出引數。  
  
-   呼叫該函式時，必須將診斷資訊格式化，並以**SQLGetDiagRec**和**SQLGetDiagField**的輸出引數傳回。  
  
 對於一個非驅動程式管理員的 ODBC 元件：  
  
-   必須根據原生錯誤來設定 SQLSTATE。 對於以檔案為基礎的驅動程式和不使用閘道的 DBMS 型驅動程式，驅動程式必須設定 SQLSTATE。 針對使用閘道的 DBMS 型驅動程式，可能是驅動程式或支援 ODBC 的閘道會設定 SQLSTATE。

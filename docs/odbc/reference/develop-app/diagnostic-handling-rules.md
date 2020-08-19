---
description: 診斷處理規則
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3112f6db31a4369ec880e31a7bb8be6e15071bed
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424660"
---
# <a name="diagnostic-handling-rules"></a>診斷處理規則
下列規則會管理 **SQLGetDiagRec** 和 **SQLGetDiagField**中的診斷處理。  
  
 針對所有 ODBC 元件：  
  
-   不得取代、改變或遮罩從另一個 ODBC 元件收到的錯誤或警告。  
  
-   當收到來自另一個 ODBC 元件的診斷訊息時，可能會新增其他狀態記錄。 新增的記錄必須將實際的資訊值新增至原始訊息。  
  
 針對直接介面資料來源的 ODBC 元件：  
  
-   必須在其廠商識別碼、其元件識別碼和資料來源識別碼之前加上其從資料來源接收的診斷訊息。  
  
-   必須保留資料來源的原生錯誤碼。  
  
-   必須保留資料來源的診斷訊息。  
  
 針對產生與資料來源無關之錯誤或警告的任何 ODBC 元件：  
  
-   必須為錯誤或警告提供正確的 SQLSTATE。  
  
-   必須產生診斷訊息的文字。  
  
-   必須在診斷訊息的廠商識別碼和其元件識別碼前面加上前置詞。  
  
-   必須傳回原生錯誤碼（如果有的話），而且有意義。  
  
 針對與驅動程式管理員互動的 ODBC 元件：  
  
-   必須初始化 **SQLGetDiagRec** 和 **SQLGetDiagField**的輸出引數。  
  
-   當呼叫該函式時，必須格式化並傳回診斷資訊，作為 **SQLGetDiagRec** 和 **SQLGetDiagField** 的輸出引數。  
  
 針對驅動程式管理員以外的一個 ODBC 元件：  
  
-   必須根據原生錯誤來設定 SQLSTATE。 針對以檔案為基礎的驅動程式和不使用閘道的 DBMS 驅動程式，驅動程式必須設定 SQLSTATE。 如果是使用閘道的 DBMS 驅動程式，則驅動程式或支援 ODBC 的閘道可能會設定 SQLSTATE。

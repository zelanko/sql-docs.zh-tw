---
title: 診斷處理規則 |微軟文件
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
ms.openlocfilehash: 9f7f9d19a5a369e9da0efbc0d62f8e556b0597c1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305839"
---
# <a name="diagnostic-handling-rules"></a>診斷處理規則
以下規則管理**SQLGetDiagRec**和**SQLGetDiagField**中的診斷處理。  
  
 對所有 ODBC 元件:  
  
-   不得替換、更改或掩蓋從其他 ODBC 元件接收的錯誤或警告。  
  
-   當他們收到來自其他 ODBC 元件的診斷消息時,可能會添加其他狀態記錄。 添加的記錄必須向原始郵件添加真實資訊值。  
  
 對直接介面資料來源的 ODBC 元件:  
  
-   必須為其供應商識別碼、其元件標識碼和資料源標識符前置碼到其從資料來源接收的診斷訊息。  
  
-   必須保留數據源的本機錯誤代碼。  
  
-   必須保留數據源的診斷消息。  
  
 對獨立於資料來源產生錯誤或警告的任何 ODBC 元件:  
  
-   必須為錯誤或警告提供正確的 SQLSTATE。  
  
-   必須生成診斷消息的文本。  
  
-   必須將其供應商識別碼和元件標識符首碼到診斷消息。  
  
-   必須返回本機錯誤代碼(如果代碼可用且有意義)。  
  
 對於與驅動程式管理員介面的 ODBC 元件:  
  
-   必須初始化**SQLGetDiagRec**和**SQLGetDiagField**的輸出參數。  
  
-   在調用該函數時,必須格式化診斷資訊並將其返回為**SQLGetDiagRec**和**SQLGetDiagField**的輸出參數。  
  
 匯出驅動程式管理員的一個 ODBC 元件:  
  
-   必須基於本機錯誤設置 SQLSTATE。 對於不使用閘道的基於檔的驅動程式和基於 DBMS 的驅動程式,驅動程式必須設置 SQLSTATE。 對於使用閘道的基於 DBMS 的驅動程式,驅動程式或支援 ODBC 的閘道可能會設置 SQLSTATE。

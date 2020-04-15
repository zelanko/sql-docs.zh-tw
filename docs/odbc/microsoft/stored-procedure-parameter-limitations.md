---
title: 儲存過程參數限制 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], stored procedures
ms.assetid: 8b804bcf-4cce-4e6f-aa45-00bab9ef9921
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bbd748884575791d5f170e95bc5aa465b61624b7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299198"
---
# <a name="stored-procedure-parameter-limitations"></a>預存程序參數限制
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 而是使用 Oracle 提供的 ODBC 驅動程式。  
  
 當執行使用 10 個或更多輸出參數的 Oracle 儲存過程時,儲存過程呼叫將失敗,從而導致存取衝突或 ActiveX 資料物件 (ADO) 錯誤。 當使用適用於 Oracle 的 Microsoft ODBC 驅動程式(適用於 Oracle 用戶端軟體的版本 8.0.4.0.0 和 8.0.4.0.4)時,可能會發生這種情況。  
  
 要更正此問題,必須將 Oracle 用戶端軟體升級到版本 8.0.4.2.0 或更高版本。 有關[修補程式](../../odbc/microsoft/oracle-software-patches.md)的更多資訊,請聯繫甲骨文公司。  
  
> [!NOTE]  
>  早期發佈 Oracle 用戶端軟體版本 8.0.3.0.0 時不會出現此問題。

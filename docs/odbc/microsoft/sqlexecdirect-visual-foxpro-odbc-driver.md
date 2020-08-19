---
description: SQLExecDirect (Visual FoxPro ODBC Driver)
title: SQLExecDirect (Visual FoxPro ODBC Driver) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLExecDirect function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 5004060f-8510-4018-87a4-d41789e69d3e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d12218097caf6d4a2c4a0375f1a8e9542b2ccf59
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449180"
---
# <a name="sqlexecdirect-visual-foxpro-odbc-driver"></a>SQLExecDirect (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特定的資訊。 如需此函數的一般資訊，請參閱 [ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的適當主題。  
  
 支援： Full  
  
 ODBC API 一致性：核心層級  
  
 執行新的 [PREPARABLE SQL 語句](../../odbc/microsoft/visual-foxpro-terminology.md)。 如果語句中有任何參數，則 Visual FoxPro ODBC 驅動程式會使用參數標記變數目前的值。  
  
 若要建立一個批次命令，一次提交一個以上的 SQL 語句，請使用分號 (; ) 以分隔批次中的每個 SQL 語句。  
  
 如果您的資料表、視圖或功能變數名稱包含空格，請用引號括住名稱。 例如，如果您的資料庫包含名為 [我的資料表] 和 [我的欄位] 欄位的資料表，請將識別碼的每個元素括起來，如下所示：  
  
```  
SELECT `My Table`.`Field1`, `My Table`.`Field2` FROM `My Table`  
```  
  
 如需詳細資訊，請參閱《 *ODBC 程式設計人員參考*》中的[SQLExecDirect](../../odbc/reference/syntax/sqlexecdirect-function.md) 。

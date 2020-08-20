---
description: SQLPrepare (Visual FoxPro ODBC Driver)
title: SQLPrepare (Visual FoxPro ODBC Driver) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLPrepare function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 0c4cb5a4-9729-4b2e-a0c6-52027b92e8fc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b8dfda2e04711681144e4a5cd21e445570e30a1b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500151"
---
# <a name="sqlprepare-visual-foxpro-odbc-driver"></a>SQLPrepare (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特定的資訊。 如需此函數的一般資訊，請參閱 [ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的適當主題。  
  
 支援： Full  
  
 ODBC API 一致性：核心層級  
  
 規劃如何優化和執行語句，以準備 SQL 語句。 [SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md)會編譯 SQL 語句以供執行。  
  
 如果您的資料表、視圖或功能變數名稱包含空格，請用引號括住名稱 (') 標記。 例如，如果您的資料庫包含名為 [我的資料表] 和 [我的欄位] 欄位的資料表，請將識別碼的每個元素括起來，如下所示：  
  
```  
SELECT * FROM `My Table`.`My Field`  
```  
  
 如需詳細資訊，請參閱《 *ODBC 程式設計人員參考*》中的[SQLPrepare](../../odbc/reference/syntax/sqlprepare-function.md) 。

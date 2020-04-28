---
title: SQLPrepare （Visual FoxPro ODBC Driver） |Microsoft Docs
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
ms.openlocfilehash: 14c9358d04e539eb2c77a00e195e8216cd0f5496
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301554"
---
# <a name="sqlprepare-visual-foxpro-odbc-driver"></a>SQLPrepare (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特有的資訊。 如需此函數的一般資訊，請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)底下的適當主題。  
  
 支援：完整  
  
 ODBC API 一致性：核心層級  
  
 藉由規劃如何優化和執行語句來準備 SQL 語句。 [SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md)會編譯 SQL 語句以供執行。  
  
 如果您的資料表、視圖或功能變數名稱包含空格，請將名稱括在後引號（'）標記中。 例如，如果您的資料庫包含名為「我的資料表」的資料表和「我的欄位」欄位，請將識別碼的每個元素括起來，如下所示：  
  
```  
SELECT * FROM `My Table`.`My Field`  
```  
  
 如需詳細資訊，請參閱 ODBC 程式設計*人員參考*中的[SQLPrepare](../../odbc/reference/syntax/sqlprepare-function.md) 。

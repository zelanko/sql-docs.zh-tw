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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5835ddaf27d097dcfff608649f50c1f7f41a93df
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67996312"
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

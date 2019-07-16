---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5835ddaf27d097dcfff608649f50c1f7f41a93df
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67996312"
---
# <a name="sqlprepare-visual-foxpro-odbc-driver"></a>SQLPrepare (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支援：完整  
  
 ODBC API 相容性：核心層級  
  
 規劃如何最佳化和執行陳述式會準備 SQL 陳述式。 執行 SQL 陳述式編譯[SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md)。  
  
 如果您的資料表、 檢視或欄位名稱包含空格，括住名稱後引號 （'） 標記。 例如，如果您的資料庫包含名為我的資料表和欄位的 我的欄位的資料表，括住識別項的每個項目，如下所示：  
  
```  
SELECT * FROM `My Table`.`My Field`  
```  
  
 如需詳細資訊，請參閱 < [SQLPrepare](../../odbc/reference/syntax/sqlprepare-function.md)中*ODBC 程式設計人員參考*。

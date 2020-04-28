---
title: SQLExecDirect （Visual FoxPro ODBC Driver） |Microsoft Docs
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
ms.openlocfilehash: 40c0a3404a3e7a9a67b6f71d197343eddb417955
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298668"
---
# <a name="sqlexecdirect-visual-foxpro-odbc-driver"></a>SQLExecDirect (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特有的資訊。 如需此函數的一般資訊，請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)底下的適當主題。  
  
 支援：完整  
  
 ODBC API 一致性：核心層級  
  
 執行新的[PREPARABLE SQL 語句](../../odbc/microsoft/visual-foxpro-terminology.md)。 如果語句中有任何參數，Visual FoxPro ODBC 驅動程式會使用參數標記變數的目前值。  
  
 若要建立一個批次命令，一次提交一個以上的 SQL 語句，請使用分號（;)以分隔批次中的每個 SQL 語句。  
  
 如果您的資料表、視圖或功能變數名稱包含空格，請將名稱括在後引號中。 例如，如果您的資料庫包含名為「我的資料表」的資料表和「我的欄位」欄位，請將識別碼的每個元素括起來，如下所示：  
  
```  
SELECT `My Table`.`Field1`, `My Table`.`Field2` FROM `My Table`  
```  
  
 如需詳細資訊，請參閱 ODBC 程式設計*人員參考*中的[SQLExecDirect](../../odbc/reference/syntax/sqlexecdirect-function.md) 。

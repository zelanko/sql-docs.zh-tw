---
title: SQLExecDirect(可視化福克斯Pro ODBC驅動程式) |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298668"
---
# <a name="sqlexecdirect-visual-foxpro-odbc-driver"></a>SQLExecDirect (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 特定於驅動程式的資訊。 有關此功能的一般資訊,請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的相應主題。  
  
 支援: 完整  
  
 ODBC API 一致性:核心等級  
  
 執行新的[可預準備 SQL 語句](../../odbc/microsoft/visual-foxpro-terminology.md)。 如果語句中存在任何參數,Visual FoxPro ODBC 驅動程式將使用參數標記變數的當前值。  
  
 要建立批次處理指令以一次提交多個 SQL 語句,請使用分號(;)分隔批次處理中的每個 SQL 語句。  
  
 如果表、檢視或欄位名稱包含空格,請將名稱包含在回引號中。 例如,如果資料庫包含名為「我的表」的表和欄位「我的欄位」,請按照如下方式包含標識符的每個元素:  
  
```  
SELECT `My Table`.`Field1`, `My Table`.`Field2` FROM `My Table`  
```  
  
 有關詳細資訊,請參閱*ODBC 程式師參考*中的[SQLExecDirect。](../../odbc/reference/syntax/sqlexecdirect-function.md)

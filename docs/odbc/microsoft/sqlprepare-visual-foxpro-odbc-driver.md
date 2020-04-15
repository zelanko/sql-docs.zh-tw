---
title: SQL準備(可視化福克斯Pro ODBC驅動程式) |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301554"
---
# <a name="sqlprepare-visual-foxpro-odbc-driver"></a>SQLPrepare (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 特定於驅動程式的資訊。 有關此功能的一般資訊,請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的相應主題。  
  
 支援: 完整  
  
 ODBC API 一致性:核心等級  
  
 通過規劃如何優化和執行該語句來準備 SQL 語句。 SQL 語句編譯供[SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md)執行。  
  
 如果表、檢視或欄位名稱包含空格,請將名稱包含在後引號 (『) 標記中。 例如,如果資料庫包含名為「我的表」的表和欄位「我的欄位」,請按照如下方式包含標識符的每個元素:  
  
```  
SELECT * FROM `My Table`.`My Field`  
```  
  
 有關詳細資訊,請參閱*ODBC 程式師參考中的* [SQLPrepare。](../../odbc/reference/syntax/sqlprepare-function.md)

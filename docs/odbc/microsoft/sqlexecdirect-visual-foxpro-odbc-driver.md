---
title: SQLExecDirect （Visual FoxPro ODBC 驅動程式） |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLExecDirect function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 5004060f-8510-4018-87a4-d41789e69d3e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b2089fb2289110ba175e4446f372c8a968b82a2e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sqlexecdirect-visual-foxpro-odbc-driver"></a>SQLExecDirect （Visual FoxPro ODBC 驅動程式）
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC 應用程式開發介面參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支援： 完整  
  
 ODBC 應用程式開發介面相容性： 核心層級  
  
 執行新[可準備 SQL 陳述式](../../odbc/microsoft/visual-foxpro-terminology.md)。 Visual FoxPro ODBC 驅動程式會使用目前的參數標記變數值，如果陳述式中存在的任何參數。  
  
 若要建立批次命令送出多個 SQL 陳述式一次，請使用分號 （;） 來分隔批次中的每個 SQL 陳述式。  
  
 如果您的資料表、 檢視或欄位名稱包含空格，括住名稱後方括號標記。 例如，如果您的資料庫包含名為 我的資料表和欄位 My Field 的資料表，括住的識別項的每個項目，如下所示：  
  
```  
SELECT `My Table`.`Field1`, `My Table`.`Field2` FROM `My Table`  
```  
  
 如需詳細資訊，請參閱[SQLExecDirect](../../odbc/reference/syntax/sqlexecdirect-function.md)中*ODBC 程式設計人員參考*。

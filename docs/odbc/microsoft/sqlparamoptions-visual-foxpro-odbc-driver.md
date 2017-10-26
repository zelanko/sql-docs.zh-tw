---
title: "SQLParamOptions （Visual FoxPro ODBC 驅動程式） |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLParamOptions function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 7f94a6e2-9c34-405c-b2b0-304d94269715
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 17a82974d8531d0524f4bac89701d6c97a05198d
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlparamoptions-visual-foxpro-odbc-driver"></a>SQLParamOptions （Visual FoxPro ODBC 驅動程式）
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC 應用程式開發介面參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支援： 完整  
  
 ODBC 應用程式開發介面相容性： 層級 1  
  
 允許應用程式指定多個值所指派的參數集[SQLBindParameter](../../odbc/microsoft/sqlbindparameter-visual-foxpro-odbc-driver.md)。 指定一組參數的多個值的能力可用於大量插入以及其他需要處理相同的 SQL 陳述式多次使用不同的參數值的資料來源的工作項目。 例如，應用程式可以指定三組值的相關聯的參數集**插入**陳述式，然後執行**插入**insert 陳述式，一次執行的三個作業。  
  
 如需詳細資訊，請參閱[SQLParamOptions](../../odbc/reference/syntax/sqlparamoptions-function.md)中*ODBC 程式設計人員參考*。


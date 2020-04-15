---
title: SQLParamOptions(可視化福克斯Pro ODBC驅動程式) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLParamOptions function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 7f94a6e2-9c34-405c-b2b0-304d94269715
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dd714ce7774265a2afd00d42894d644a516bc402
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299468"
---
# <a name="sqlparamoptions-visual-foxpro-odbc-driver"></a>SQLParamOptions (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 特定於驅動程式的資訊。 有關此功能的一般資訊,請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的相應主題。  
  
 支援: 完整  
  
 ODBC API 符合性:1 級  
  
 允許應用程式為[SQLBind 參數](../../odbc/microsoft/sqlbindparameter-visual-foxpro-odbc-driver.md)分配的參數集指定多個值。 為一組參數指定多個值的能力對於批量插入和其他需要數據源使用各種參數值多次處理同一 SQL 語句的工作非常有用。 例如,應用程式可以為與**INSERT**語句關聯的參數集指定三組值,然後執行一次**INSERT**語句以執行三個插入操作。  
  
 有關詳細資訊,請參閱*ODBC 程式師參考*中的[SQLParamOptions。](../../odbc/reference/syntax/sqlparamoptions-function.md)

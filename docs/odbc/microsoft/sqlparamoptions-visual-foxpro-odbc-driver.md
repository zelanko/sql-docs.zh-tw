---
description: SQLParamOptions (Visual FoxPro ODBC Driver)
title: SQLParamOptions (Visual FoxPro ODBC Driver) |Microsoft Docs
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
ms.openlocfilehash: e40af7f0bb03c0b5245717880e67e72b38559aed
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500191"
---
# <a name="sqlparamoptions-visual-foxpro-odbc-driver"></a>SQLParamOptions (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特定的資訊。 如需此函數的一般資訊，請參閱 [ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的適當主題。  
  
 支援： Full  
  
 ODBC API 一致性：層級1  
  
 允許應用程式為 [SQLBindParameter](../../odbc/microsoft/sqlbindparameter-visual-foxpro-odbc-driver.md)指派的參數集合指定多個值。 針對一組參數指定多個值的能力，對於大量插入和其他需要資料來源使用各種參數值多次處理相同 SQL 語句的工作而言很有用。 例如，應用程式可以為一組與 **insert** 語句相關聯的參數指定三組值，然後執行 **insert** 語句一次，以執行三個插入作業。  
  
 如需詳細資訊，請參閱《 *ODBC 程式設計人員參考*》中的[SQLParamOptions](../../odbc/reference/syntax/sqlparamoptions-function.md) 。

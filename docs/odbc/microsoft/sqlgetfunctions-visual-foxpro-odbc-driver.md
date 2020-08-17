---
description: SQLGetFunctions (Visual FoxPro ODBC Driver)
title: SQLGetFunctions (Visual FoxPro ODBC Driver) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetFunctions function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 8102932a-88b3-49d8-bf7a-c766f54878c0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: df1413b657ec4631390525a702a625ba480e9f7e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340114"
---
# <a name="sqlgetfunctions-visual-foxpro-odbc-driver"></a>SQLGetFunctions (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特定的資訊。 如需此函數的一般資訊，請參閱 [ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的適當主題。  
  
 支援： Full  
  
 ODBC API 一致性：層級1  
  
 針對所有支援的函數傳回 TRUE。  
  
 Visual FoxPro ODBC 驅動程式支援所有 ODBC API 核心和層級1函數。 下表指出驅動程式是否支援特定的層級2函數。  
  
|*Function*|支援|  
|----------------|---------------|  
|SQL_API_SQLBROWSECONNECT|否|  
|SQL_API_SQLCOLUMNPRIVELEGES|否|  
|SQL_API_SQLDATASOURCES|是|  
|SQL_API_SQLDESCRIBEPARAM|否|  
|SQL_API_SQLDRIVERS|是|  
|SQL_API_SQLEXTENDEDFETCH|是|  
|SQL_API_SQLFOREIGNKEYS|否|  
|SQL_API_SQLMORERESULTS|是|  
|SQL_API_SQLNATIVESQL|否|  
|SQL_API_SQLNUMPARAMS|是|  
|SQL_API_SQLPARAMOPTIONS|是|  
|SQL_API_SQLPRIMARYKEYS|是|  
|SQL_API_SQLPROCEDURECOLUMNS|否|  
|SQL_API_SQLPROCEDURES|否|  
|SQL_API_SQLSETPOS|是|  
|SQL_API_SQLSETSCROLLOPTIONS|是|  
|SQL_API_SQLTABLEPRIVILEGES|否|  
  
 如需詳細資訊，請參閱《 *ODBC 程式設計人員參考*》中的[SQLGetFunctions](../../odbc/reference/syntax/sqlgetfunctions-function.md) 。

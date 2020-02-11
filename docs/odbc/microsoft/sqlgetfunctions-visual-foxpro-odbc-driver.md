---
title: SQLGetFunctions （Visual FoxPro ODBC Driver） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: da74bbb64a76f6c3ff6c55754798b975dab83826
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68003328"
---
# <a name="sqlgetfunctions-visual-foxpro-odbc-driver"></a>SQLGetFunctions (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特有的資訊。 如需此函數的一般資訊，請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)底下的適當主題。  
  
 支援：完整  
  
 ODBC API 一致性：層級1  
  
 針對所有支援的函式傳回 TRUE。  
  
 Visual FoxPro ODBC 驅動程式支援所有 ODBC API 核心和層級1功能。 下表指出驅動程式是否支援特定層級2函式。  
  
|*函數*|支援|  
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
  
 如需詳細資訊，請參閱 ODBC 程式設計*人員參考*中的[SQLGetFunctions](../../odbc/reference/syntax/sqlgetfunctions-function.md) 。

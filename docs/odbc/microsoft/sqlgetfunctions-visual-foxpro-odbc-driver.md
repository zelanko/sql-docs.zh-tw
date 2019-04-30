---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e0ae7b8eb0468dd401009ef58c83b87606b0679a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63313072"
---
# <a name="sqlgetfunctions-visual-foxpro-odbc-driver"></a>SQLGetFunctions (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支援：完整  
  
 ODBC API 相容性：層級 1  
  
 傳回所有支援的函式，則為 TRUE。  
  
 Visual FoxPro ODBC 驅動程式支援所有 ODBC API 的核心和層級 1 的函式。 下表會指出驅動程式是否支援特定的層級 2 函式。  
  
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
  
 如需詳細資訊，請參閱 < [SQLGetFunctions](../../odbc/reference/syntax/sqlgetfunctions-function.md)中*ODBC 程式設計人員參考*。

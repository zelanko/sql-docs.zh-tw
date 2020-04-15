---
title: SQL程式列(訪問驅動程式) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLProcedureColumns
- SQLProcedureColumns function [ODBC], Access Driver
ms.assetid: 34fee995-5848-4ecb-bda0-fc362a77b2d9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: be17776ac6b6879140a7c57bede1b3cb539d97be
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299458"
---
# <a name="sqlprocedurecolumns-access-driver"></a>SQLProcedureColumns (Access 驅動程式)
> [!NOTE]  
>  本主題提供特定於訪問驅動程序的資訊。 有關此功能的一般資訊,請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的相應主題。  
  
 應用程式開發人員應查找從結果集末尾開始並向後移動的驅動程式定義的列。  
  
|資料行|註解|  
|------------|--------------|  
|COLUMN_TYPE|SQL_PARAM_INPUT或SQL_RESULT_COL|  
|序|這是在結果集末尾返回的特定於驅動程式的列。 列的 SQL 類型是整數。|

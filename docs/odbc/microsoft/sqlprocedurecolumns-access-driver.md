---
title: SQLProcedureColumns （Access 驅動程式） |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299458"
---
# <a name="sqlprocedurecolumns-access-driver"></a>SQLProcedureColumns (Access 驅動程式)
> [!NOTE]  
>  本主題提供存取驅動程式特定的資訊。 如需此函數的一般資訊，請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)底下的適當主題。  
  
 應用程式開發人員應該從結果集的結尾開始尋找驅動程式定義的資料行，然後繼續回溯。  
  
|資料行|評價|  
|------------|--------------|  
|COLUMN_TYPE|SQL_PARAM_INPUT 或 SQL_RESULT_COL|  
|序列|這是在結果集結尾傳回的驅動程式特定的資料行。 資料行的 SQL 類型是整數。|

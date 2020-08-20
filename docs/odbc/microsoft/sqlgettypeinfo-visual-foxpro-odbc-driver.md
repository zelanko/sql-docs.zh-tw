---
description: SQLGetTypeInfo (Visual FoxPro ODBC Driver)
title: SQLGetTypeInfo (Visual FoxPro ODBC Driver) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 5f25e20b-a4ef-42da-aeb6-00e0510fb1cc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e24f506f1134e9191e370971795a23bbbb3bd380
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500173"
---
# <a name="sqlgettypeinfo-visual-foxpro-odbc-driver"></a>SQLGetTypeInfo (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特定的資訊。 如需此函數的一般資訊，請參閱 [ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的適當主題。  
  
 支援： Full  
  
 ODBC API 一致性：層級1  
  
 傳回資料來源所支援資料類型的相關資訊。 驅動程式會傳回 SQL 結果集中的資訊。 下表列出 ODBC 資料類型和對應的 Visual FoxPro 資料類型。  
  
|ODBC 型別|Visual FoxPro 類型|  
|---------------|------------------------|  
|SQL_BIGINT|不支援。 沒有64位的 Visual FoxPro 類型。|  
|SQL_BIT|邏輯|  
|SQL_CHAR|字元|  
|SQL_DATE|Date|  
|SQL_DECIMAL|數值|  
|SQL_DOUBLE|Double|  
|SQL_FLOAT|Double|  
|SQL_INTEGER|整數|  
|SQL_LONGVARBINARY| (二進位) 的備註|  
|SQL_LONGVARCHAR|備忘錄|  
|SQL_NUMERIC|數值 *、貨幣、浮點數|  
|SQL_REAL|Double|  
|SQL_SMALLINT|整數|  
|SQL_TIME|不支援。 沒有任何 Visual FoxPro *時間* 類型。|  
|SQL_TIMESTAMP|Datetime|  
|SQL_TINYINT|整數|  
|SQL_VARBINARY| (二進位) *、一般的備註|  
|SQL_VARCHAR|字元|  
  
 * 預設類型  
  
 如需有關 Visual FoxPro 資料類型的詳細資訊，請參閱 [CREATE TABLE](../../odbc/microsoft/create-table-sql-command.md)。 如需此函數的詳細資訊，請參閱《 *ODBC 程式設計人員參考*》中的[SQLGetTypeInfo](../../odbc/reference/syntax/sqlgettypeinfo-function.md) 。

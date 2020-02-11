---
title: SQLGetTypeInfo （Visual FoxPro ODBC Driver） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f29be5e03a6cc9c1c91809db2b8ec7c686e90f11
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67898624"
---
# <a name="sqlgettypeinfo-visual-foxpro-odbc-driver"></a>SQLGetTypeInfo (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特有的資訊。 如需此函數的一般資訊，請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)底下的適當主題。  
  
 支援：完整  
  
 ODBC API 一致性：層級1  
  
 傳回資料來源所支援之資料類型的相關資訊。 驅動程式會傳回 SQL 結果集中的資訊。 下表列出 ODBC 資料類型和對應的 Visual FoxPro 資料類型。  
  
|ODBC 類型|Visual FoxPro 類型|  
|---------------|------------------------|  
|SQL_BIGINT|不支援。 沒有64位的 Visual FoxPro 類型。|  
|SQL_BIT|邏輯|  
|SQL_CHAR|字元|  
|SQL_DATE|Date|  
|SQL_DECIMAL|數值|  
|SQL_DOUBLE|DOUBLE|  
|SQL_FLOAT|DOUBLE|  
|SQL_INTEGER|整數|  
|SQL_LONGVARBINARY|備忘（二進位）|  
|SQL_LONGVARCHAR|備忘錄|  
|SQL_NUMERIC|Numeric *、Currency、Float|  
|SQL_REAL|DOUBLE|  
|SQL_SMALLINT|整數|  
|SQL_TIME|不支援。 沒有 Visual FoxPro*時間*類型。|  
|SQL_TIMESTAMP|Datetime|  
|SQL_TINYINT|整數|  
|SQL_VARBINARY|備忘（二進位） *，一般|  
|SQL_VARCHAR|字元|  
  
 * 預設類型  
  
 如需有關 Visual FoxPro 資料類型的詳細資訊，請參閱[CREATE TABLE](../../odbc/microsoft/create-table-sql-command.md)。 如需此函數的詳細資訊，請參閱 ODBC 程式設計*人員參考*中的[SQLGetTypeInfo](../../odbc/reference/syntax/sqlgettypeinfo-function.md) 。

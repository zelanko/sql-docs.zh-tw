---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 05cc6dc2647b5297b8d7176cd4bc70261b78cb71
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47733056"
---
# <a name="sqlgettypeinfo-visual-foxpro-odbc-driver"></a>SQLGetTypeInfo (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支援： 完整  
  
 ODBC API 相容性： 層級 1  
  
 傳回資料來源所支援的資料類型的相關資訊。 驅動程式中的 SQL 結果集傳回的資訊。 下表列出 ODBC 資料類型和對應的 Visual FoxPro 資料型別。  
  
|ODBC 類型|Visual FoxPro 類型|  
|---------------|------------------------|  
|SQL_BIGINT|不支援。 沒有任何 64 位元 Visual FoxPro 型別。|  
|SQL_BIT|邏輯|  
|SQL_CHAR|字元|  
|SQL_DATE|date|  
|SQL_DECIMAL|數值|  
|SQL_DOUBLE|Double|  
|SQL_FLOAT|Double|  
|SQL_INTEGER|Integer|  
|SQL_LONGVARBINARY|備忘 （二進位）|  
|SQL_LONGVARCHAR|備忘錄|  
|SQL_NUMERIC|數值 *，貨幣、 Float|  
|SQL_REAL|Double|  
|SQL_SMALLINT|Integer|  
|SQL_TIME|不支援。 沒有任何 Visual FoxPro*時間*型別。|  
|SQL_TIMESTAMP|DateTime|  
|SQL_TINYINT|Integer|  
|SQL_VARBINARY|備忘 （二進位） *、 一般|  
|SQL_VARCHAR|字元|  
  
 * 預設類型  
  
 如需 Visual FoxPro 資料類型的詳細資訊，請參閱[CREATE TABLE](../../odbc/microsoft/create-table-sql-command.md)。 如需有關這個函式的詳細資訊，請參閱 < [SQLGetTypeInfo](../../odbc/reference/syntax/sqlgettypeinfo-function.md)中*ODBC 程式設計人員參考*。

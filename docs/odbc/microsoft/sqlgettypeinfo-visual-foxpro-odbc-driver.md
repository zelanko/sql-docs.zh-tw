---
title: SQLGetTypeInfo(可視化福克斯Pro ODBC驅動程式) |微軟文件
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
ms.openlocfilehash: 23db0350f0f7271f85e2bc5c6a9e6c8767443a85
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299518"
---
# <a name="sqlgettypeinfo-visual-foxpro-odbc-driver"></a>SQLGetTypeInfo (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 特定於驅動程式的資訊。 有關此功能的一般資訊,請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的相應主題。  
  
 支援: 完整  
  
 ODBC API 符合性:1 級  
  
 返回有關數據源支援的數據類型的資訊。 驅動程式返回 SQL 結果集中的資訊。 下表列出了 ODBC 數據類型和相應的 Visual FoxPro 資料類型。  
  
|ODBC 型別|視覺化狐狸專業類型|  
|---------------|------------------------|  
|SQL_BIGINT|不支援。 沒有 64 位可視化福克斯專業類型。|  
|SQL_BIT|邏輯|  
|SQL_CHAR|字元|  
|SQL_DATE|Date|  
|SQL_DECIMAL|數值|  
|SQL_DOUBLE|Double|  
|SQL_FLOAT|Double|  
|SQL_INTEGER|整數|  
|SQL_LONGVARBINARY|備忘錄(二進位)|  
|SQL_LONGVARCHAR|備忘錄|  
|SQL_NUMERIC|數位*, 貨幣, 浮動|  
|SQL_REAL|Double|  
|SQL_SMALLINT|整數|  
|SQL_TIME|不支援。 沒有可視化 FoxPro*時間*類型。|  
|SQL_TIMESTAMP|Datetime|  
|SQL_TINYINT|整數|  
|SQL_VARBINARY|備忘錄(二進位)*,一般|  
|SQL_VARCHAR|字元|  
  
 *預設類型  
  
 有關 Visual FoxPro 資料類型的詳細資訊,請參閱[建立表](../../odbc/microsoft/create-table-sql-command.md)格 。 有關此功能的詳細資訊,請參閱*ODBC 程式師參考*中的[SQLGetTypeInfo。](../../odbc/reference/syntax/sqlgettypeinfo-function.md)

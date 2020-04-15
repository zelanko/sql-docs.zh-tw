---
title: SQLGetTypeInfo(Excel 驅動程式) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC], Excel Driver
- Excel driver [ODBC], SQLGetTypeInfo
ms.assetid: 708845be-e6a1-4677-8113-c52819a43fa4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 64befe30be9ed7988e0c9348e9335eb632dd975c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81295068"
---
# <a name="sqlgettypeinfo-excel-driver"></a>SQLGetTypeInfo (Excel 驅動程式)
> [!NOTE]  
>  本主題提供特定於 Excel 驅動程式的資訊。 有關此功能的一般資訊,請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的相應主題。  
  
 **SQLGetTypeInfo**生成的表中返回的類型(TYPE_NAME)的名稱將是數據源最常用的名稱。  
  
 SQL_ALL_EXCEPT_LIKE將在位元組、計數器、雙、單、長和短資料類型的 SEARCHABLE 列中返回。 (可以通過使用 ODBC 規範轉換函數將值轉換為字元,然後執行比較來實現 LIKE 功能。  
  
 使用 Microsoft Excel 驅動程式時,ODBC 類型名稱將傳回**在 SQLGetTypeInfo**返回的TYPE_NAME列中。

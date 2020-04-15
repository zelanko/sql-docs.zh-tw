---
title: SQLGetTypeInfo(文字檔案驅動程式) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC], Text File Driver
- text file driver [ODBC], SQLGetTypeInfo
ms.assetid: 05a58975-093c-4bd9-bd72-b5f0026a6e36
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7b70b58e4760959db102450b5f8b7beed042df95
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294998"
---
# <a name="sqlgettypeinfo-text-file-driver"></a>SQLGetTypeInfo (文字檔驅動程式)
> [!NOTE]  
>  本主題提供特定於文本檔驅動程序的資訊。 有關此功能的一般資訊,請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的相應主題。  
  
 **SQLGetTypeInfo**生成的表中返回的類型(TYPE_NAME)的名稱將是數據源最常用的名稱。  
  
 SQL_ALL_EXCEPT_LIKE將在位元組、計數器、雙、單、長和短資料類型的 SEARCHABLE 列中返回。 (可以通過使用 ODBC 規範轉換函數將值轉換為字元,然後執行比較來實現 LIKE 功能。  
  
 使用文本驅動程式時 **,SQLGetTypeInfo**會為文本資料類型(CHAR 和 LONGCHAR)返回 FALSE 的CASE_SENSITIVE值,當資料類型實際上區分大小寫時。

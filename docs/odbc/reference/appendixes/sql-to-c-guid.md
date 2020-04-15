---
title: 'SQL 到 C: GUID |微軟文件'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to C types [ODBC], GUID
- data conversions from SQL to C types [ODBC], guid
- GUID data type [ODBC]
ms.assetid: cf56c684-c261-4b89-994a-db14ab2241d6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f0f247bc4cb411d535050d7c78e0ea42cc144b0e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296458"
---
# <a name="sql-to-c-guid"></a>SQL 到 C：GUID
GUID ODBC SQL 資料類型的識別碼是:  
  
 SQL_GUID  
  
 下表顯示了可轉換為 GUID SQL 資料的 ODBC C 資料類型。 有關表中列與字語的說明,請參考[資料從 SQL 轉換為 C 資料型態](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  
  
|C 類型識別碼|測試|**目標價值Ptr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*緩衝區長度*>字符字节长度|資料|36|n/a|  
||*緩衝區長度*< 37|未定義|未定義|22003|  
|SQL_C_WCHAR|*緩衝區長度*>字符长度|資料|36|n/a|  
||*緩衝區長度*< 37|未定義|未定義|22003|  
|SQL_C_BINARY|資料\<= *緩衝區長度*的位元組長度|資料|以位元組為單位的資料長度|n/a|  
||>*緩衝區長度*的資料位元組長度|未定義|未定義|22003|  
|SQL_C_GUID|無[a]|資料|16[b]|n/a|  
  
 [a] 此轉換將忽略*緩衝區長度*的值。 驅動程式假定 **目標價值Ptr*的大小是 C 資料類型的大小。  
  
 [b] 這是相應的 C 資料類型的大小。

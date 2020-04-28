---
title: SQL 到 C： GUID |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81296458"
---
# <a name="sql-to-c-guid"></a>SQL 到 C：GUID
GUID ODBC SQL 資料類型的識別碼為：  
  
 SQL_GUID  
  
 下表顯示可轉換 GUID SQL 資料的 ODBC C 資料類型。 如需資料表中的資料行和詞彙的說明，請參閱將[資料從 SQL 轉換成 C 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  
  
|C 類型識別碼|測試|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > 字元位元組長度|資料|36|n/a|  
||*BufferLength* < 37|未定義|未定義|22003|  
|SQL_C_WCHAR|*BufferLength* > 字元長度|資料|36|n/a|  
||*BufferLength* < 37|未定義|未定義|22003|  
|SQL_C_BINARY|資料\< =  *BufferLength*的位元組長度|資料|資料長度（以位元組為單位）|n/a|  
||資料 > *BufferLength*的位元組長度|未定義|未定義|22003|  
|SQL_C_GUID|無 [a]|資料|16 [b]|n/a|  
  
 [a] 這項轉換會忽略*BufferLength*的值。 驅動程式假設 **TargetValuePtr*的大小是 C 資料類型的大小。  
  
 [b] 這是對應 C 資料類型的大小。

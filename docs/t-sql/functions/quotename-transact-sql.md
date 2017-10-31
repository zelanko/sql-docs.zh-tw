---
title: "QUOTENAME (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- QUOTENAME_TSQL
- QUOTENAME
dev_langs:
- TSQL
helpviewer_keywords:
- delimited identifiers [SQL Server]
- input strings [SQL Server]
- Unicode [SQL Server], delimited identifiers
- QUOTENAME function
- valid identifiers [SQL Server]
ms.assetid: 34d47f1e-2ac7-4890-8c9c-5f60f115e076
caps.latest.revision: 35
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7f4e40797fc49e8a70b01162fc6959ad60475e8b
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="quotename-transact-sql"></a>QUOTENAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回 Unicode 字串，且附加了分隔符號，以便使輸入字串成為有效的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 分隔識別碼。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
QUOTENAME ( 'character_string' [ , 'quote_character' ] )   
```  
  
## <a name="arguments"></a>引數  
 '*character_string*'  
 這是 Unicode 字元資料的字串。 *character_string*是**sysname** ，長度限制為 128 個字元。 大於 128 個字元的輸入會傳回 NULL。  
  
 '*quote_character*'  
 這是用來當做分隔符號的單字元字串。 可以是單引號 ( **'** )、 左或右方括號 ( **[]** )，或雙引號 ( **"** )。 如果*quote_character*未指定，會使用方括號。  
  
## <a name="return-types"></a>傳回類型  
 **nvarchar （258)**  
  
## <a name="examples"></a>範例  
 下列範例會使用字元字串 `abc[]def`，且利用 `[` 和 `]` 字元來建立有效的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 分隔識別碼。  
  
```  
SELECT QUOTENAME('abc[]def');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
[abc[]]def]  
  
(1 row(s) affected)  
```  
  
 請注意，`abc[]def` 字串中的兩個右方括號用來表示逸出字元。  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下列範例會使用字元字串 `abc def`，且利用 `[` 和 `]` 字元來建立有效的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 分隔識別碼。  
  
```  
SELECT QUOTENAME('abc def');   
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
[abc def]  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>另請參閱  
 [字串函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  



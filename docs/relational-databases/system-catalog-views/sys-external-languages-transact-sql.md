---
title: sys.external_languages (TRANSACT-SQL)-SQL Server |Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.reviewer: dphansen
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- external_languages
- external_languages_TSQL
- sys.external_languages
- sys.external_languages_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.external_languages catalog view
author: nelgson
ms.author: negust
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 1cef52f066a07032240d17f88297b02ba3f7e5fb
ms.sourcegitcommit: be09f0f3708f2e8eb9f6f44e632162709b4daff6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/21/2019
ms.locfileid: "65995116"
---
# <a name="sysexternallanguages-transact-sql"></a>sys.external_languages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

這份目錄檢視會提供資料庫中的外部語言的清單。 **R**並**Python**為保留的名稱，而且不需要外部的語言可以使用這些特定的名稱來建立。

## <a name="sysexternallanguages"></a>sys.external_languages

目錄檢視 sys.external_languages 列出每個資料庫中的外部語言的資料列。

|資料行名稱 |資料類型 | 描述|
|------|------|------|
|external_language_id |ssNoversion | 外部語言識別碼|
|language |sysname |外部語言的名稱。 在資料庫中，這是唯一的。 R 和 Python 是每個執行個體的保留的名稱|
|create_date |datetime2 |建立的日期和時間|
|principal_id |ssNoversion |擁有這個外部程式庫的主體識別碼|

## <a name="see-also"></a>另請參閱  

+ [sys.external_language_files](sys-external-language-files-transact-sql.md)  
+ [CREATE EXTERNAL LANGUAGE](../../t-sql/statements/create-external-language-transact-sql.md) 

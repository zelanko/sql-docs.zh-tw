---
title: sys. external_languages （Transact-sql）-SQL Server |Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
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
ms.reviewer: dphansen
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 225e20e199a401e544be9c86a7b05a078f556530
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85751725"
---
# <a name="sysexternal_languages-transact-sql"></a>sys.databases external_languages （Transact-sql）
[!INCLUDE[SQL Server 2019](../../includes/applies-to-version/sqlserver2019.md)]

此目錄檢視會提供資料庫中的外部語言清單。 **R** 和 **Python** 為保留的名稱，且不能使用這些特定的名稱來建立任何外部語言。

## <a name="sysexternal_languages"></a>sys.external_languages

目錄檢視 sys. external_languages 會針對資料庫中的每個外部語言列出一個資料列。

|資料行名稱 |資料類型 | 描述|
|------|------|------|
|external_language_id |int | 外部語言的識別碼|
|語言 |sysname |外部語言的名稱。 在資料庫中，這是唯一的。 R 和 Python 是每個實例的保留名稱|
|create_date |datetime2 |建立的日期和時間|
|principal_id |int |擁有此外部程式庫之主體的識別碼|

## <a name="see-also"></a>另請參閱  

+ [sys.external_language_files](sys-external-language-files-transact-sql.md)  
+ [建立外部語言](../../t-sql/statements/create-external-language-transact-sql.md) 

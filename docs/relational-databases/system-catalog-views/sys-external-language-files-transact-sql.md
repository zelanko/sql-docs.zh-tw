---
description: sys. external_language_files (Transact-sql) -SQL Server
title: sys. external_language_files (Transact-sql) -SQL Server |Microsoft Docs
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
ms.openlocfilehash: fe6da94cc085e14667ee0518452fc6043eed60e9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88401064"
---
# <a name="sysexternal_language_files-transact-sql"></a>sys. external_language_files (Transact-sql) 
[!INCLUDE[SQL Server 2019](../../includes/applies-to-version/sqlserver2019.md)]

此目錄檢視會提供資料庫中的外部語言延伸模組檔案清單。 **R** 和 **Python** 為保留的名稱，且不能使用這些特定的名稱來建立任何外部語言。

從 file_spec 建立外部語言時，此視圖中會列出延伸模組本身及其屬性。 此視圖會包含每個語言的每個作業系統一個專案。

## <a name="sysexternal_languages"></a>sys.external_languages

目錄檢視 sys. external_language_files 會列出資料庫中每個外部語言延伸模組的資料列。 參數

|資料行名稱 |資料類型 | 描述|
|------|------|------|
|external_language_id |int | 外部語言的識別碼|
|內容|varbinary(max) |外部語言擴充檔的內容|
|file_name|Nvarchar (266) |語言延伸模組檔案名|
|平台|TINYINT|安裝 SQL Server 之主機平臺的識別碼|
|platform_desc |nvarchar(60)|主機平臺的名稱。 有效的值為 ' WINDOWS '、' LINUX '。|
|參數|nvarchar(4000)|外部語言 prameters|
|environment_variables |nvarchar(4000)|外部語言環境變數|

## <a name="see-also"></a>另請參閱  

+ [sys.external_languages](sys-external-languages-transact-sql.md)  
+ [建立外部語言](../../t-sql/statements/create-external-language-transact-sql.md)  

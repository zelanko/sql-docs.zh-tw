---
title: sys. external_language_files （Transact-sql）-SQL Server |Microsoft Docs
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
ms.openlocfilehash: 0d1325311ef0b708f5a3abd5f4494e099863efc2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "65995086"
---
# <a name="sysexternal_language_files-transact-sql"></a>sys.databases external_language_files （Transact-sql）
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

此目錄檢視會提供資料庫中的外部語言擴充檔案清單。 **R**和**Python**是保留的名稱，而且不能使用這些特定名稱來建立外部語言。

從 file_spec 建立外部語言時，延伸模組本身及其屬性會列在此視圖中。 此視圖會包含每個語言、每個 OS 的一個專案。

## <a name="sysexternal_languages"></a>sys.external_languages

目錄檢視 sys. external_language_files 列出資料庫中每個外部語言擴充功能的資料列。 參數

|資料行名稱 |資料類型 | 描述|
|------|------|------|
|external_language_id |int | 外部語言的識別碼|
|內容|varbinary(max) |外部語言擴充檔案的內容|
|file_name|Nvarchar （有其）|語言擴充檔案的名稱|
|平台|tinyint|安裝 SQL Server 之主機平臺的識別碼|
|platform_desc |nvarchar(60)|主機平臺的名稱。 有效的值為 ' WINDOWS '、' LINUX '。|
|parameters|nvarchar(4000)|外部語言 prameters|
|environment_variables |nvarchar(4000)|外部語言環境變數|

## <a name="see-also"></a>另請參閱  

+ [sys.external_languages](sys-external-languages-transact-sql.md)  
+ [建立外部語言](../../t-sql/statements/create-external-language-transact-sql.md)  

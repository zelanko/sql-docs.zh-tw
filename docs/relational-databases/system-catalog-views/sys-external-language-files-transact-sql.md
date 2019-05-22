---
title: sys.external_language_files (TRANSACT-SQL)-SQL Server |Microsoft Docs
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
ms.sourcegitcommit: be09f0f3708f2e8eb9f6f44e632162709b4daff6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/21/2019
ms.locfileid: "65995086"
---
# <a name="sysexternallanguagefiles-transact-sql"></a>sys.external_language_files & Amp;#40;transact-SQL&AMP;#41;
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

這份目錄檢視會提供資料庫中的外部語言延伸模組檔案的清單。 **R**並**Python**為保留的名稱，而且不需要外部的語言可以使用這些特定的名稱來建立。

從 file_spec 建立外部的語言時，延伸模組本身和它的屬性會列在這個檢視中。 此檢視會包含每種語言，每個作業系統的一個項目。

## <a name="sysexternallanguages"></a>sys.external_languages

目錄檢視 sys.external_language_files 列出每個資料庫中的外部語言擴充功能的資料列。 參數

|資料行名稱 |資料類型 | 描述|
|------|------|------|
|external_language_id |ssNoversion | 外部語言識別碼|
|content|varbinary(max) |外部語言延伸模組檔案的內容|
|file_name|nvarchar(266)|語言擴充功能檔案的名稱|
|平台|TINYINT|SQL Server 安裝所在的主機平台的識別碼|
|platform_desc |nvarchar(60)|主機平台的名稱。 有效值為 'WINDOWS'，'LINUX'。|
|參數|nvarchar(4000)|外部語言 prameters|
|environment_variables |nvarchar(4000)|外部語言環境變數|

## <a name="see-also"></a>另請參閱  

+ [sys.external_languages](sys-external-languages-transact-sql.md)  
+ [CREATE EXTERNAL LANGUAGE](../../t-sql/statements/create-external-language-transact-sql.md)  

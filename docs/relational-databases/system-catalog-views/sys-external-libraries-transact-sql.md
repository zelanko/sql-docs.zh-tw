---
title: sys.external_libraries (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 10/05/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- external_libraries
- external_libraries_TSQL
- sys.external_libraries
- sys.external_libraries_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.external_libraries catalog view
author: HeidiSteen
ms.author: heidist
manager: cgronlun
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 19704a37c9f34ee3b27bdee962246d98c0b18e71
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47796616"
---
# <a name="sysexternallibraries-transact-sql"></a>sys.external_libraries & Amp;#40;transact-SQL&AMP;#41;  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]


支援與外部執行階段，例如 R 或 Python 的套件程式庫的管理。

## <a name="sysexternallibraries"></a>sys.external_libraries

目錄檢視 sys.external_libraries 列出每個已上傳到資料庫的外部程式庫的資料列。

|資料行名稱 |資料類型 | 描述|
|------|------|------|
|external_library_id |ssNoversion | 外部程式庫物件的識別碼。 |
|NAME |sysname |外部程式庫的名稱。 是每個擁有者在資料庫內唯一的。|
|principal_id |ssNoversion |擁有這個外部程式庫的主體識別碼。 |
|language | sysname | 支援的外部程式庫的執行階段之語言的名稱。 有效值為 'R'。 其他的執行階段可能會在未來新增。|
|範圍 (scope) |ssNoversion |公用的範圍內; 01 代表私用範圍 |  
|scope_desc |varchar(7) |指出封裝是否為公用或私用|


## <a name="see-also"></a>另請參閱  
[sys.external_library_files](sys-external-library-files-transact-sql.md)  
[建立外部程式庫](../../t-sql/statements/create-external-library-transact-sql.md)  
[SQL Server R services 套件管理](../../advanced-analytics/r/installing-and-managing-r-packages.md)  

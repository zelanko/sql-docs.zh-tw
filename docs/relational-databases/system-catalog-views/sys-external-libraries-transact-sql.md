---
title: sys.external_libraries (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 10/05/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
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
author: jeannt
ms.author: jeannt
manager: craigg
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: d8fa8a4d41cff452379c420b712f13b2d4415a74
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sysexternallibraries-transact-sql"></a>sys.external_libraries (TRANSACT-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]


支援與外部執行階段，例如 R 或 Python 封裝程式庫的管理。

## <a name="sysexternallibraries"></a>sys.external_libraries

目錄檢視 sys.external_libraries 列出每個已上傳到資料庫的外部程式庫的資料列。

|資料行名稱 |資料類型 | Description|
|------|------|------|
|external_library_id |int | 外部程式庫物件的識別碼。 |
|name |sysname |外部程式庫的名稱。 是每個擁有者在資料庫內唯一的。|
|principal_id |int |擁有這個外部的程式庫的主體識別碼。 |
|language | sysname | 語言或執行階段支援的外部程式庫的名稱。 有效值為 'R'。 可能在未來新增其他執行階段。|
|範圍 (scope) |int |0 代表公用的範圍內。私用範圍 1 |  
|scope_desc |varchar(7) |指出封裝是否為公用或私用|


## <a name="see-also"></a>另請參閱  
[sys.external_library_files](sys-external-library-files-transact-sql.md)  
[建立外部程式庫](../../t-sql/statements/create-external-library-transact-sql.md)  
[SQL Server R services 的封裝管理](../../advanced-analytics/r/installing-and-managing-r-packages.md)  

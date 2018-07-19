---
title: sys.external_libraries (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 10/05/2017
ms.prod: sql
ms.prod_service: database-engine
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
ms.openlocfilehash: 110f514c4688536decfd29c412ce310746cd972e
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38001190"
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

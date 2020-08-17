---
description: sys.external_libraries (Transact-SQL)
title: sys. external_libraries (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/25/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: machine-learning
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
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 6dcc1b8f7cddc785203dc2430c2f1a4dce4b4d39
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88377574"
---
# <a name="sysexternal_libraries-transact-sql"></a>sys.external_libraries (Transact-SQL)  
[!INCLUDE [SQL Server 2017 SQL MI](../../includes/applies-to-version/sqlserver2017-asdbmi.md)]

支援管理與外部執行時間相關的套件程式庫，例如 R、Python 和 JAVA。

> [!NOTE]
> 在 SQL Server 2017 中，支援 R 語言和 Windows 平台。 SQL Server 2019 及更新版本支援 Windows 和 Linux 平台上的 R、Python 和 Java。 在 Azure SQL 受控執行個體上，支援 R 和 Python。

## <a name="sysexternal_libraries"></a>sys.external_libraries

目錄檢視 sys. external_libraries 會針對已上傳至資料庫的每個外部程式庫，列出一個資料列。

|資料行名稱 |資料類型 | 描述|
|------|------|------|
|external_library_id |int | 外部程式庫物件的識別碼。 |
|NAME |sysname |外部程式庫的名稱。 在每個擁有者的資料庫中都是唯一的。|
|principal_id |int |擁有此外部程式庫之主體的識別碼。 |
|語言 | sysname | 支援外部程式庫的語言或執行時間名稱。 有效的值為 ' R '、' Python ' 和 ' JAVA '。 未來可能會加入其他執行時間。|
|scope |int |0代表公用範圍;1代表私用範圍 |  
|scope_desc |Varchar (7)  |指出封裝是否為公用或私用|

## <a name="see-also"></a>另請參閱  

+ [sys.external_library_files](sys-external-library-files-transact-sql.md)  
+ [建立外部程式庫](../../t-sql/statements/create-external-library-transact-sql.md)  
+ [安裝新的 R 套件](../../machine-learning/package-management/install-additional-r-packages-on-sql-server.md)  
+ [安裝新的 Python 套件](../../machine-learning/package-management/install-additional-python-packages-on-sql-server.md)  

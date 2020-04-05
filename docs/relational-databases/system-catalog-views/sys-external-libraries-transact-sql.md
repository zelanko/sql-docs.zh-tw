---
title: 系統external_libraries(轉用-SQL) |微軟文件
ms.custom: ''
ms.date: 11/04/2019
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
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6b1bfc00b403fa76f692db78593ed4c0e6b53ce8
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/04/2020
ms.locfileid: "80664429"
---
# <a name="sysexternal_libraries-transact-sql"></a>sys.external_libraries (Transact-SQL)  
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

支援管理與外部運行時(如 R、Python 和 JAVA)相關的包庫。

> [!NOTE]
> 在 SQL Server 2017 中，支援 R 語言和 Windows 平台。 SQL Server 2019 及更新版本支援 Windows 和 Linux 平台上的 R、Python 和 Java。

## <a name="sysexternal_libraries"></a>sys.external_libraries

目錄檢視 sys.external_libraries列出已上傳到資料庫的每個外部庫的行。

|資料行名稱 |資料類型 | 描述|
|------|------|------|
|external_library_id |int | 外部庫物件的識別碼。 |
|NAME |sysname |外部庫的名稱。 每個擁有者的資料庫中是唯一的。|
|principal_id |int |擁有此外部庫的委託人 ID。 |
|語言 | sysname | 支援外部庫的語言或運行時的名稱。 有效值為"R"、"Python"和"Java"。 將來可能會添加其他運行時。|
|scope |int |0 表示公共範圍;1 表示專用範圍 |  
|scope_desc |瓦爾查爾(7) |指示包是公共包還是私有包|

## <a name="see-also"></a>另請參閱  

+ [sys.external_library_files](sys-external-library-files-transact-sql.md)  
+ [建立外部函式庫](../../t-sql/statements/create-external-library-transact-sql.md)  
+ [在 SQL Server 上安裝新的 R 套件](../../machine-learning/package-management/install-additional-r-packages-on-sql-server.md)  
+ [在 SQL Server 上安裝新的 Python 套件](../../machine-learning/package-management/install-additional-python-packages-on-sql-server.md)  
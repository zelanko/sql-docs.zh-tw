---
title: sys.external_libraries (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/27/2018
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
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f0c24f7a95a7146f4d67d655ec0ed5ec58a53ace
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58492362"
---
# <a name="sysexternallibraries-transact-sql"></a>sys.external_libraries (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

支援與外部執行階段，例如 R、 Python 和 Java 套件程式庫的管理。

> [!NOTE]
> 在 SQL Server 2017 中，支援 R 語言和 Windows 平台。 SQL Server 2019 CTP 2.4 支援 R、 Python 和 Java 的 Windows 和 Linux 平台上。

## <a name="sysexternallibraries"></a>sys.external_libraries

目錄檢視 sys.external_libraries 列出每個已上傳到資料庫的外部程式庫的資料列。

|資料行名稱 |資料類型 | 描述|
|------|------|------|
|external_library_id |ssNoversion | 外部程式庫物件的識別碼。 |
|NAME |sysname |外部程式庫的名稱。 是每個擁有者在資料庫內唯一的。|
|principal_id |ssNoversion |擁有這個外部程式庫的主體識別碼。 |
|language | sysname | 支援的外部程式庫的執行階段之語言的名稱。 有效值為 'R'、 'Python' 和 'Java'。 其他的執行階段可能會在未來新增。|
|範圍 (scope) |ssNoversion |公用的範圍內; 01 代表私用範圍 |  
|scope_desc |varchar(7) |指出封裝是否為公用或私用|

## <a name="see-also"></a>另請參閱  

+ [sys.external_library_files](sys-external-library-files-transact-sql.md)  
+ [CREATE EXTERNAL LIBRARY](../../t-sql/statements/create-external-library-transact-sql.md)  
+ [在 SQL Server 上安裝新的 R 套件](../../advanced-analytics/r/install-additional-r-packages-on-sql-server.md)  
+ [在 SQL Server 上安裝新的 Python 套件](../../advanced-analytics/python/install-additional-python-packages-on-sql-server.md)  
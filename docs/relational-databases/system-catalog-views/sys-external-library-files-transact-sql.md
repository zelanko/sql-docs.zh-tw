---
title: sys.external_library_files (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 10/05/2017
ms.prod: sql
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- external_library_files
- external_library_files_TSQL
- sys.external_library_files
- sys.external_library_files_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.external_library_files catalog view
author: HeidiSteen
ms.author: heidist
manager: cgronlun
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a9666b58132feb79876c4e8074dc530440c05b2c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "68220340"
---
# <a name="sysexternallibraryfiles-transact-sql"></a>sys.external_library_files & Amp;#40;transact-SQL&AMP;#41;  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

列出每個檔案的外部程式庫所組成的資料列。

|資料行名稱 |資料類型 |描述|
|------|------|-----|
|external_library_id | ssNoversion |外部程式庫物件的識別碼。 |
|content |varbinary(max) |外部程式庫檔案成品的內容。 |
|平台 |TINYINT |SQL Server 安裝所在的主機平台的識別碼。 |
|platform_desc | nvarchar(60) |主機平台的名稱。 有效值為 'WINDOWS'，'LINUX'。 |

### <a name="see-also"></a>另請參閱  

[sys.external_libraries](sys-external-libraries-transact-sql.md)  
[建立外部程式庫](../../t-sql/statements/create-external-library-transact-sql.md)  
[SQL Server Machine Learning 服務的套件管理](../../advanced-analytics/r/installing-and-managing-r-packages.md)  

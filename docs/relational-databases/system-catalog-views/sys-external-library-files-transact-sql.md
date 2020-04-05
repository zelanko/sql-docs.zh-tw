---
title: 系統external_library_files(轉算-SQL) |微軟文件
ms.custom: ''
ms.date: 07/24/2019
ms.prod: sql
ms.technology: machine-learning
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
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b2f1bbdc3936dc6295b9ecc51b937e50cae20670
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/04/2020
ms.locfileid: "80664233"
---
# <a name="sysexternal_library_files-transact-sql"></a>sys.external_library_files (Transact-SQL)  
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

列出組成外部庫的每個檔的行。

|資料行名稱 |資料類型 |描述|
|------|------|-----|
|external_library_id | int |外部庫物件的識別碼。 |
|content |varbinary(max) |外部庫文件項目的內容。 |
|平台 |TINYINT |安裝 SQL Server 的主機平台的 ID。 |
|platform_desc | nvarchar(60) |主機平臺的名稱。 有效值為"WINDOWS","LINUX"。 |

### <a name="see-also"></a>另請參閱  

[sys.external_libraries](sys-external-libraries-transact-sql.md)  
[建立外部函式庫](../../t-sql/statements/create-external-library-transact-sql.md)  


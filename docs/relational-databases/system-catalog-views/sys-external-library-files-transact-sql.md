---
title: "sys.external_library_files (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 10/05/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
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
author: jeannt
ms.author: jeannt
manager: craigg
ms.openlocfilehash: cf8a1b59827c53bc4ae04f76dbe7084a4ad828d4
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2018
---
# <a name="sysexternallibraryfiles-transact-sql"></a>sys.external_library_files (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

列出外部程式庫所組成的每個檔案的資料列。

|資料行名稱 |資料類型 |Description|
|------|------|-----|
|external_library_id | int |外部程式庫物件的識別碼。 |
|content |varbinary(max) |外部程式庫檔案成品的內容。 |
|平台 |tinyint |安裝 SQL Server 的主機平台的識別碼。 |
|platform_desc | nvarchar(60) |主機平台的名稱。 有效值為 'WINDOWS'、 'LINUX'。 |

### <a name="see-also"></a>另請參閱  

[sys.external_libraries](sys-external-libraries-transact-sql.md)  
[建立外部程式庫](../../t-sql/statements/create-external-library-transact-sql.md)  
[SQL Server 機器學習服務封裝管理](../../advanced-analytics/r/installing-and-managing-r-packages.md)  

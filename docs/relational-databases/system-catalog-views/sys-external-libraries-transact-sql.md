---
title: external_libraries (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 07/24/2019
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
ms.openlocfilehash: 78923a0eb1404c1437c6e1144888261e542ebc5a
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2019
ms.locfileid: "68471105"
---
# <a name="sysexternallibraries-transact-sql"></a>external_libraries (Transact-sql)  
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

支援管理與外部執行時間 (例如 R、Python 和 JAVA) 相關的套件程式庫。

> [!NOTE]
> 在 SQL Server 2017 中，支援 R 語言和 Windows 平台。 在 SQL Server 2019 CTP 2.4 中，支援 Windows 和 Linux 平台上的 R、Python 和 Java。

## <a name="sysexternallibraries"></a>sys.external_libraries

目錄檢視 external_libraries 會針對每個已上傳至資料庫的外部程式庫列出一個資料列。

|資料行名稱 |資料類型 | 描述|
|------|------|------|
|external_library_id |ssNoversion | 外部程式庫物件的識別碼。 |
|name |sysname |外部程式庫的名稱。 在資料庫中, 每個擁有者都是唯一的。|
|principal_id |ssNoversion |擁有此外部程式庫之主體的識別碼。 |
|language | sysname | 支援外部程式庫的語言或執行時間名稱。 有效值為「R」、「Python」和「JAVA」。 未來可能會加入其他執行時間。|
|scope |ssNoversion |0代表公用範圍;1代表私用範圍 |  
|scope_desc |Varchar (7) |指出封裝為公用或私用。|

## <a name="see-also"></a>另請參閱  

+ [sys.external_library_files](sys-external-library-files-transact-sql.md)  
+ [建立外部程式庫](../../t-sql/statements/create-external-library-transact-sql.md)  
+ [在 SQL Server 上安裝新的 R 套件](../../advanced-analytics/r/install-additional-r-packages-on-sql-server.md)  
+ [在 SQL Server 上安裝新的 Python 套件](../../advanced-analytics/python/install-additional-python-packages-on-sql-server.md)  
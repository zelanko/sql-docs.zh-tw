---
description: sys.trusted_assemblies (Transact-SQL)
title: sys. trusted_assemblies (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- trusted_assemblies_TSQL
- trusted_assemblies
- sys.trusted_assemblies_TSQL
- sys.trusted_assemblies
dev_langs:
- TSQL
helpviewer_keywords:
- sys.trusted_assemblies
ms.assetid: ''
author: VanMSFT
ms.author: vanto
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e4eee138db35efe4b8f9b01f88d07b52141ab9a1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88475158"
---
# <a name="systrusted_assemblies-transact-sql"></a>sys.trusted_assemblies (Transact-SQL)  
[!INCLUDE[SQL Server 2017](../../includes/applies-to-version/sqlserver2017.md)]

針對伺服器的每個受信任元件，各包含一個資料列。

 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  


|資料行名稱 |資料類型 |描述 |
|--- |--- |--- |
|雜湊 |varbinary(8000) |元件內容 SHA2_512 雜湊。 |
|description |nvarchar(4000) |元件的選擇性使用者定義描述。 Microsoft 建議使用正式名稱，以將簡單名稱、版本號碼、文化特性、公開金鑰，以及要信任之元件的架構編碼。 此值可唯一識別 common language runtime 上的元件 (CLR) 端，與 sys. 元件中的 clr_name 值相同。 |
|create_date |datetime2 |將元件新增至受信任元件清單的日期。 |
|created_by |nvarchar(128) |將元件加入至清單之主體的登入名稱。 |
| | | |


## <a name="remarks"></a>備註  

您 **可以使用 [新增 sp_add_trusted_assembly** ] 和 [ **需要加入 sys. trusted_assemblies** 新增或移除元件 `sys.trusted_assemblies` 。

## <a name="see-also"></a>另請參閱  
  [sys. sp_add_trusted_assembly](../../relational-databases/system-stored-procedures/sys-sp-add-trusted-assembly-transact-sql.md) [sys. sp_drop_trusted_assembly](../../relational-databases/system-stored-procedures/sys-sp-drop-trusted-assembly-transact-sql.md) [drop assembly &#40;transact-sql&#41;](../../t-sql/statements/drop-assembly-transact-sql.md)  
  [sys.assemblies](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)  
  [sys.dm_clr_loaded_assemblies](../../relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql.md)  


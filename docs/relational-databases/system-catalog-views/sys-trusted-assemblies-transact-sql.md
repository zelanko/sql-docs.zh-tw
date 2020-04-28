---
title: sys.databases trusted_assemblies （Transact-sql） |Microsoft Docs
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
ms.openlocfilehash: 9682535c82f8a579259993e82560dfe6bc930f93
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68061357"
---
# <a name="systrusted_assemblies-transact-sql"></a>sys.trusted_assemblies (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

針對伺服器的每個受信任元件，各包含一個資料列。

 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  


|資料行名稱 |資料類型 |描述 |
|--- |--- |--- |
|雜湊 |varbinary(8000) |元件內容的 SHA2_512 雜湊。 |
|description |nvarchar(4000) |選擇性的使用者定義元件描述。 Microsoft 建議使用將簡單名稱、版本號碼、文化特性、公開金鑰和元件的架構編碼成信任的正式名稱。 這個值會唯一識別 common language runtime （CLR）端的元件，而且與 sys.databases 中的 clr_name 值相同。 |
|create_date |datetime2 |將元件加入至受信任元件清單的日期。 |
|created_by |nvarchar(128) |將元件加入清單中之主體的登入名稱。 |
| | | |


## <a name="remarks"></a>備註  

使用 [**需要] 加入 sp_add_trusted_assembly** ，而且**需要加入 trusted_assemblies**新增或移除元件`sys.trusted_assemblies`。

## <a name="see-also"></a>另請參閱  
  [sp_add_trusted_assembly](../../relational-databases/system-stored-procedures/sys-sp-add-trusted-assembly-transact-sql.md) [sys. sp_drop_trusted_assembly](../../relational-databases/system-stored-procedures/sys-sp-drop-trusted-assembly-transact-sql.md) [drop assembly &#40;transact-sql&#41;](../../t-sql/statements/drop-assembly-transact-sql.md)  
  [sys.assemblies](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)  
  [sys.dm_clr_loaded_assemblies](../../relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql.md)  


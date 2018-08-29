---
title: sys.trusted_assemblies (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
manager: craigg
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 989233e4e13a26b316a554a908a1282d384565f6
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43081081"
---
# <a name="systrustedassemblies-transact-sql"></a>sys.trusted_assemblies & Amp;#40;transact-SQL&AMP;#41;  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

包含一個資料列，每個受信任的組件中的伺服器。

 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  


|資料行名稱 |資料類型 |描述 |
|--- |--- |--- |
|hash (雜湊) |varbinary(8000) |組件內容 SHA2_512 雜湊。 |
|description |nvarchar(4000) |使用者定義的選擇性描述組件。 Microsoft 建議使用的簡單名稱、 版本號碼、 文化特性、 公開金鑰和要信任的組件的架構會將編碼的正式名稱。 這個值會唯一識別 common language runtime (CLR) 端上的組件，而且是 sys.assemblies clr_name 值相同。 |
|create_date |datetime2 |組件加入至受信任的組件清單的日期。 |
|created_by |& lt;languagekeyword>nvarchar(128)</languagekeyword&gt |組件新增至清單之主體的登入名稱。 |
| | | |


## <a name="remarks"></a>備註  

使用**需要新增 sp_add_trusted_assembly**並**需要新增 sys.trusted_assemblies**新增或移除組件從`sys.trusted_assemblies`。

## <a name="see-also"></a>另請參閱  
  [sys.sp_add_trusted_assembly](../../relational-databases/system-stored-procedures/sys-sp-add-trusted-assembly-transact-sql.md) [sys.sp_drop_trusted_assembly](../../relational-databases/system-stored-procedures/sys-sp-drop-trusted-assembly-transact-sql.md) [卸除組件&#40;-SQL&AMP;#41;&#41;](../../t-sql/statements/drop-assembly-transact-sql.md)  
  [sys.assemblies](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)  
  [sys.dm_clr_loaded_assemblies](../../relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql.md)  


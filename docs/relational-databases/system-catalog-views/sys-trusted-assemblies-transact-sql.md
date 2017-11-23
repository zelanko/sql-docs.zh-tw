---
title: "sys.trusted_assemblies (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- trusted_assemblies_TSQL
- trusted_assemblies
- sys.trusted_assemblies_TSQL
- sys.trusted_assemblies
dev_langs: TSQL
helpviewer_keywords: sys.trusted_assemblies
ms.assetid: 
caps.latest.revision: 
author: tmullaney
ms.author: thmullan;rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2ef97b33df620457102d79ad9535a3550014aa55
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="systrustedassemblies-transact-sql"></a>sys.trusted_assemblies (TRANSACT-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

伺服器的每一個受信任的組件包含一個資料列。

 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  


|資料行名稱 |資料類型 |Description |
|--- |--- |--- |
|hash (雜湊) |varbinary （8000) |組件內容 SHA2_512 雜湊。 |
|description |nvarchar(4000) |選擇性使用者定義描述組件。 Microsoft 建議使用的簡單名稱、 版本號碼、 文化特性、 公開金鑰和要信任的組件的架構會將編碼的正式名稱。 這個值會唯一識別組件的 common language runtime (CLR) 端上，而且是 sys.assemblies clr_name 值相同。 |
|create_date |datetime2 |組件加入至信任的組件清單的日期。 |
|created_by |nvarchar （128) |組件加入至清單之主體的登入名稱。 |
| | | |


## <a name="remarks"></a>備註  

使用**需要加入 sp_add_trusted_assembly**和**需要加入 sys.trusted_assemblies**新增或移除組件從`sys.trusted_assemblies`。

## <a name="see-also"></a>請參閱＜  
  [sys.sp_add_trusted_assembly](../../relational-databases/system-stored-procedures/sys-sp-add-trusted-assembly-transact-sql.md) [sys.sp_drop_trusted_assembly](../../relational-databases/system-stored-procedures/sys-sp-drop-trusted-assembly-transact-sql.md) [卸除組件 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-assembly-transact-sql.md)  
  [sys.assemblies](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)  
  [sys.dm_clr_loaded_assemblies](../../relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql.md)  


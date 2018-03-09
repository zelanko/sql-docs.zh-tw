---
title: "sys.sp_drop_trusted_assembly (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_drop_trusted_assembly_TSQL
- sp_drop_trusted_assembly
- sys.sp_drop_trusted_assembly_TSQL
- sys.sp_drop_trusted_assembly
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_drop_trusted_assembly
ms.assetid: 
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c04f2992d0f715d95eda631de97dd6e8eb3dac72
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="sysspdroptrustedassembly-transact-sql"></a>sys.sp_drop_trusted_assembly (TRANSACT-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

從伺服器上的受信任組件清單中卸除組件。

 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  


## <a name="syntax"></a>語法
```  
sp_drop_trusted_assembly 
    [ @hash = ] 'value'
```  

## <a name="arguments"></a>引數

[ @hash =] '*值*'  
從伺服器受信任的組件清單中卸除組件的 SHA2_512 雜湊值。 啟用 clr 嚴格的安全性，即使組件是不帶正負號或資料庫不標示為值得信任時，可能會載入受信任的組件。

## <a name="remarks"></a>備註  

此程序中移除組件從[sys.trusted_assemblies](../../relational-databases/system-catalog-views/sys-trusted-assemblies-transact-sql.md)。

## <a name="permissions"></a>Permissions

需要的成員資格`sysadmin`固定的伺服器角色或`CONTROL SERVER`權限。

## <a name="examples"></a>範例  

下列範例會從受信任的組件的伺服器清單，卸除組件雜湊。  

```  
EXEC sp_drop_trusted_assembly 
0x8893AD6D78D14EE43DF482E2EAD44123E3A0B684A8873C3F7BF3B5E8D8F09503F3E62370CE742BBC96FE3394477214B84C7C1B0F7A04DCC788FA99C2C09DFCCC; 
```  

## <a name="see-also"></a>請參閱＜  
  [sys.sp_add_trusted_assembly](sys-sp-add-trusted-assembly-transact-sql.md) [sys.trusted_assemblies](../../relational-databases/system-catalog-views/sys-trusted-assemblies-transact-sql.md) [卸除組件 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-assembly-transact-sql.md)  
  [sys.assemblies](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)  
  [sys.dm_clr_loaded_assemblies](../../relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql.md)  


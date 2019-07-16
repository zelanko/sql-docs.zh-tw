---
title: sys.sp_drop_trusted_assembly (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
ms.assetid: ''
author: VanMSFT
ms.author: vanto
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 50385161b417d02db2dc44ad1172910d31f198b3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67905143"
---
# <a name="sysspdroptrustedassembly-transact-sql"></a>sys.sp_drop_trusted_assembly & Amp;#40;transact-SQL&AMP;#41;  
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
從伺服器的受信任組件清單中卸除組件的 SHA2_512 雜湊值。 啟用 clr 嚴格安全性時，即使是不帶正負號的組件或資料庫不會標示為值得信任，可能會載入受信任的組件。

## <a name="remarks"></a>備註  

此程序中移除組件從[sys.trusted_assemblies](../../relational-databases/system-catalog-views/sys-trusted-assemblies-transact-sql.md)。

## <a name="permissions"></a>Permissions

需要的成員資格`sysadmin`固定的伺服器角色或`CONTROL SERVER`權限。

## <a name="examples"></a>範例  

下列範例會從伺服器的受信任組件清單，卸除組件雜湊。  

```  
EXEC sp_drop_trusted_assembly 
0x8893AD6D78D14EE43DF482E2EAD44123E3A0B684A8873C3F7BF3B5E8D8F09503F3E62370CE742BBC96FE3394477214B84C7C1B0F7A04DCC788FA99C2C09DFCCC; 
```  

## <a name="see-also"></a>另請參閱  
  [sys.sp_add_trusted_assembly](sys-sp-add-trusted-assembly-transact-sql.md) [sys.trusted_assemblies](../../relational-databases/system-catalog-views/sys-trusted-assemblies-transact-sql.md) [卸除組件&#40;-SQL&AMP;#41;&#41;](../../t-sql/statements/drop-assembly-transact-sql.md)  
  [sys.assemblies](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)  
  [sys.dm_clr_loaded_assemblies](../../relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql.md)  


---
title: sys.databases sp_add_trusted_assembly （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_trusted_assembly_TSQL
- sp_add_trusted_assembly
- sys.sp_add_trusted_assembly_TSQL
- sys.sp_add_trusted_assembly
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_add_trusted_assembly
ms.assetid: ''
author: VanMSFT
ms.author: vanto
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bb34a814780a46c12c65948bd0b552effaacda4d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "72452883"
---
# <a name="syssp_add_trusted_assembly-transact-sql"></a>sys.sp_add_trusted_assembly (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdbmi-xxxx-xxx-md.md)]

將元件加入至伺服器的受信任元件清單。

 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  


## <a name="syntax"></a>語法
```  
sp_add_trusted_assembly 
    [ @hash = ] 'value'
    [ , [ @description = ] 'description' ]
```  

## <a name="remarks"></a>備註  

此程式會將元件加入至[sys. trusted_assemblies](../../relational-databases/system-catalog-views/sys-trusted-assemblies-transact-sql.md)。

## <a name="arguments"></a>引數

[ @hash = ]'*value*'  
要加入至伺服器之受信任元件清單的元件 SHA2_512 雜湊值。 當[CLR strict 安全性](../../database-engine/configure-windows/clr-strict-security.md)啟用時，即使元件不帶正負號或資料庫未標示為值得信任，也可能會載入受信任的元件。

[ @description = ][*描述*]  
選擇性的使用者定義元件描述。 Microsoft 建議使用將簡單名稱、版本號碼、文化特性、公開金鑰和元件的架構編碼成信任的正式名稱。 這個值會唯一識別 common language runtime （CLR）端的元件，而且與 sys.databases 中的 clr_name 值相同。 

## <a name="permissions"></a>權限

需要固定伺服器角色`sysadmin`或`CONTROL SERVER`許可權中的成員資格。

## <a name="examples"></a>範例  

下列範例會將名`pointudt`為的元件加入至伺服器的受信任元件清單。 這些值可從[sys.databases](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)取得。     

```  
EXEC sp_add_trusted_assembly 0x8893AD6D78D14EE43DF482E2EAD44123E3A0B684A8873C3F7BF3B5E8D8F09503F3E62370CE742BBC96FE3394477214B84C7C1B0F7A04DCC788FA99C2C09DFCCC, 
N'pointudt, version=0.0.0.0, culture=neutral, publickeytoken=null, processorarchitecture=msil';
```  

## <a name="see-also"></a>另請參閱  
  [sys. sp_drop_trusted_assembly](sys-sp-drop-trusted-assembly-transact-sql.md)  
  [sys. trusted_assemblies](../../relational-databases/system-catalog-views/sys-trusted-assemblies-transact-sql.md)  
  [CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)  
  [CLR 嚴格安全性](../../database-engine/configure-windows/clr-strict-security.md)  
  [sys.assemblies](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)  
  [sys.dm_clr_loaded_assemblies](../../relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql.md)  


---
title: sys.sp_add_trusted_assembly (TRANSACT-SQL) |Microsoft Docs
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
manager: craigg
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6c7cbcd065f2cb86522d057246226570ba3dad66
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47630646"
---
# <a name="sysspaddtrustedassembly-transact-sql"></a>sys.sp_add_trusted_assembly & Amp;#40;transact-SQL&AMP;#41;  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

將組件加入至伺服器的受信任組件清單中。

 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  


## <a name="syntax"></a>語法
```  
sp_add_trusted_assembly 
    [ @hash = ] 'value'
    [ , [ @description = ] 'description' ]
```  

## <a name="remarks"></a>備註  

此程序加入至組件[sys.trusted_assemblies](../../relational-databases/system-catalog-views/sys-trusted-assemblies-transact-sql.md)。

## <a name="arguments"></a>引數

[ @hash =] '*值*'  
要新增至伺服器的受信任組件清單的組件 SHA2_512 雜湊值。 受信任的組件可能會載入的時機[CLR 嚴格安全性](../../database-engine/configure-windows/clr-strict-security.md)已啟用，即使是不帶正負號的組件或資料庫不會標示為值得信任。

[ @description =] '*描述*'  
使用者定義的選擇性描述組件。 Microsoft 建議使用的簡單名稱、 版本號碼、 文化特性、 公開金鑰和要信任的組件的架構會將編碼的正式名稱。 這個值會唯一識別 common language runtime (CLR) 端上的組件，而且是 sys.assemblies clr_name 值相同。 

## <a name="permissions"></a>Permissions

需要的成員資格`sysadmin`固定的伺服器角色或`CONTROL SERVER`權限。

## <a name="examples"></a>範例  

下列範例會將名為組件`pointudt`至伺服器的受信任組件的清單。 這些值都是從[sys.assemblies](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)。     

```  
EXEC sp_add_trusted_assembly 0x8893AD6D78D14EE43DF482E2EAD44123E3A0B684A8873C3F7BF3B5E8D8F09503F3E62370CE742BBC96FE3394477214B84C7C1B0F7A04DCC788FA99C2C09DFCCC, 
N'pointudt, version=0.0.0.0, culture=neutral, publickeytoken=null, processorarchitecture=msil';
```  

## <a name="see-also"></a>另請參閱  
  [sys.sp_drop_trusted_assembly](sys-sp-drop-trusted-assembly-transact-sql.md)  
  [sys.trusted_assemblies](../../relational-databases/system-catalog-views/sys-trusted-assemblies-transact-sql.md)  
  [CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)  
  [CLR 嚴格安全性](../../database-engine/configure-windows/clr-strict-security.md)  
  [sys.assemblies](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)  
  [sys.dm_clr_loaded_assemblies](../../relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql.md)  


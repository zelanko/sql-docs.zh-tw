---
title: sp_helpdevice (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpdevice
- sp_helpdevice_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpdevice
ms.assetid: 1a5eafa7-384e-4691-ba05-978eb73bbefb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3ec03794e60027ea578988dbe38855d8ad14cb09
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47596796"
---
# <a name="sphelpdevice-transact-sql"></a>sp_helpdevice (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  報告 Microsoft® SQL Server™ 備份裝置的相關資訊。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 我們建議您改用[sys.backup_devices](../../relational-databases/system-catalog-views/sys-backup-devices-transact-sql.md)目錄檢視。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helpdevice [ [ @devname = ] 'name' ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@devname =** ] **'***name***'**  
 這是報告的資訊所屬的備份裝置名稱。 值*名稱*總是**sysname**。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**device_name**|**sysname**|邏輯裝置名稱。|  
|**physical_name**|**nvarchar(260)**|實體檔案名稱。|  
|**description**|**nvarchar(255)**|裝置的描述。|  
|**status**|**int**|對應至狀態描述的數字**描述**資料行。|  
|**cntrltype**|**smallint**|裝置的控制器類型：<br /><br /> 2 = 磁碟裝置<br /><br /> 5 = 磁帶裝置|  
|**size**|**int**|裝置大小 (2KB) 頁面。|  
  
## <a name="remarks"></a>備註  
 如果*名稱*指定，則**sp_helpdevice**顯示指定傾印裝置的相關資訊。 如果*名稱*未指定，則**sp_helpdevice**顯示中的所有傾印裝置的相關資訊**sys.backup_devices**目錄檢視。  
  
 傾印裝置時，會新增至系統上，使用**sp_addumpdevice**。  
  
## <a name="permissions"></a>Permissions  
 需要 **public** 角色的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會報告 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體所有傾印裝置的相關資訊。  
  
```  
EXEC sp_helpdevice;  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_addumpdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)   
 [sp_dropdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdevice-transact-sql.md)   
 [Database Engine 預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

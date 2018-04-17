---
title: xp_loginconfig (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- xp_loginconfig_TSQL
- xp_loginconfig
dev_langs:
- TSQL
helpviewer_keywords:
- xp_loginconfig
ms.assetid: d380e799-2857-408a-bcbf-5e73a8e6aa5a
caps.latest.revision: 38
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 58aa7fd9d3b3ca47e93c294f9730c1a0c8d09de9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="xploginconfig-transact-sql"></a>xp_loginconfig (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  報告 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的登入安全性組態。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
xp_loginconfig ['config_name']  
```  
  
## <a name="arguments"></a>引數  
 **'** *config_name* **'**  
 這是您要顯示的組態值。 如果*config_name*是未指定，會報告所有的組態值。 *config_name*是**sysname**，預設值是 NULL，而且可以是下列值之一。  
  
|Value|Description|  
|-----------|-----------------|  
|**登入模式**|登入安全性模式。 可能的值為**混合**和**Windows 驗證**。<br /><br /> 取代者：<br /><br /> `SELECT SERVERPROPERTY('IsIntegratedSecurityOnly'); GO`|  
|**預設登入**|信任連接之授權使用者 (沒有相符登入名稱的使用者) 的預設 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入識別碼名稱。 預設登入是**客體**。 提供這個值的目的，是為了與舊版相容。|  
|**預設網域**|信任連接之網路使用者的預設 Windows 網域名稱。 預設網域就是執行 Windows 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之電腦的網域。 提供這個值的目的，是為了與舊版相容。|  
|**稽核層級**|稽核層級。 可能的值為**無**，**成功**，**失敗**，和**所有**。 稽核會寫入錯誤記錄檔和 Windows 事件檢視器中。|  
|**設定主機名稱**|指出來自用戶端登入記錄的主機名稱，是否換成 Windows 網路使用者名稱。 可能的值為**true**或**false**。 如果這個屬性設定，網路使用者名稱會出現在輸出**sp_who**。|  
|**對應 _**|報告有哪些特殊的 Windows 字元被對應至有效的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 底線字元 (_)。 可能的值為**網域分隔符號**（預設）、**空間**， **null**，或任何單一字元。 提供這個值的目的，是為了與舊版相容。|  
|**對應 $**|報告有哪些特殊的 Windows 字元被對應至有效的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 貨幣符號字元 ($)。 可能的值為**網域分隔符號**，**空間**， **null**，或任何單一字元。 預設值是**空間**。 提供這個值的目的，是為了與舊版相容。|  
|**將對應的 #**|報告有哪些特殊的 Windows 字元被對應至有效的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 數字符號字元 (#)。 可能的值為**網域分隔符號**，**空間**， **null**，或任何單一字元。 預設值是連字號。 提供這個值的目的，是為了與舊版相容。|  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|組態值|  
|**設定值**|**sysname**|組態值設定|  
  
## <a name="remarks"></a>備註  
 **xp_loginconfig**無法用來設定組態值。  
  
 若要設定登入模式和稽核層級，請使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
## <a name="permissions"></a>Permissions  
 需要 CONTROL 權限的**主要**資料庫。  
  
## <a name="examples"></a>範例  
  
### <a name="a-how-to-report-all-configuration-values"></a>A. 如何報告所有的組態值  
 下列範例會顯示目前設定的所有設定值。  
  
```  
EXEC xp_loginconfig;  
GO  
```  
  
### <a name="b-how-to-report-a-specific-configuration-value"></a>B. 如何報告特定的組態值  
 下列範例只會顯示登入模式的設定。  
  
```  
EXEC xp_loginconfig 'login mode';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_denylogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-denylogin-transact-sql.md)   
 [sp_grantlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_revokelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [xp_logininfo &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md)  
  
  

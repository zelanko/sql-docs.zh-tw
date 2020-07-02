---
title: xp_loginconfig （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_loginconfig_TSQL
- xp_loginconfig
dev_langs:
- TSQL
helpviewer_keywords:
- xp_loginconfig
ms.assetid: d380e799-2857-408a-bcbf-5e73a8e6aa5a
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: ac7a3e57c18f6ce4ea73415224aabc3843488cf9
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85755554"
---
# <a name="xp_loginconfig-transact-sql"></a>xp_loginconfig (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

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
 這是您要顯示的組態值。 如果未指定*config_name* ，就會報告所有設定值。 *config_name*是**sysname**，預設值是 Null，它可以是下列值之一。  
  
|值|說明|  
|-----------|-----------------|  
|**登入模式**|登入安全性模式。 可能的值為**混合**式和**Windows 驗證**。<br /><br /> 取代者：<br /><br /> `SELECT SERVERPROPERTY('IsIntegratedSecurityOnly'); GO`|  
|**預設登入**|信任連接之授權使用者 (沒有相符登入名稱的使用者) 的預設 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入識別碼名稱。 預設登入為**guest**。 提供這個值的目的，是為了與舊版相容。|  
|**預設網域**|信任連接之網路使用者的預設 Windows 網域名稱。 預設網域就是執行 Windows 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之電腦的網域。 提供這個值的目的，是為了與舊版相容。|  
|**audit 層級**|稽核層級。 可能的值為 [**無**]、[**成功**]、[**失敗**] 和 [**全部**]。 稽核會寫入錯誤記錄檔和 Windows 事件檢視器中。|  
|**設定主機名稱**|指出來自用戶端登入記錄的主機名稱，是否換成 Windows 網路使用者名稱。 可能的值為**true**或**false**。 如果設定此項，網路使用者名稱會出現在**sp_who**的 [輸出] 中。|  
|**地圖**|報告有哪些特殊的 Windows 字元被對應至有效的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 底線字元 (_)。 可能的值為 [**網域分隔符號**] （預設）、[**空格**]、[ **null**] 或任何單一字元。 提供這個值的目的，是為了與舊版相容。|  
|**map $**|報告有哪些特殊的 Windows 字元被對應至有效的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 貨幣符號字元 ($)。 可能的值為**網域分隔符號**、**空格**、 **null**或任何單一字元。 預設值是**space**。 提供這個值的目的，是為了與舊版相容。|  
|**地圖#**|報告有哪些特殊的 Windows 字元被對應至有效的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 數字符號字元 (#)。 可能的值為**網域分隔符號**、**空格**、 **null**或任何單一字元。 預設值是連字號。 提供這個值的目的，是為了與舊版相容。|  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|組態值|  
|**config value**|**sysname**|組態值設定|  
  
## <a name="remarks"></a>備註  
 **xp_loginconfig**不能用來設定設定值。  
  
 若要設定登入模式和稽核層級，請使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
## <a name="permissions"></a>權限  
 需要**master**資料庫的 CONTROL 許可權。  
  
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
 [sp_denylogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-denylogin-transact-sql.md)   
 [sp_grantlogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [&#40;Transact-sql&#41;的系統預存程式](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_revokelogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [xp_logininfo &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md)  
  
  

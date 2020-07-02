---
title: sp_helpremotelogin （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpremotelogin_TSQL
- sp_helpremotelogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpremotelogin
ms.assetid: 93f50869-2627-4642-899f-8f626f8833f4
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 3e277954a16e1e63d55e54b1eadb157c7f74a667
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85729191"
---
# <a name="sp_helpremotelogin-transact-sql"></a>sp_helpremotelogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  報告本機伺服器上所定義之特定遠端伺服器，或所有遠端伺服器的遠端登入相關資訊。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)]請改用連結伺服器和連結伺服器預存程序。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helpremotelogin [ [ @remoteserver = ] 'remoteserver' ]   
     [ , [ @remotename = ] 'remote_name' ]  
```  
  
## <a name="arguments"></a>引數  
 [ @remoteserver **=** ] **'***remoteserver***'**  
 這是要傳回相關遠端登入資訊的遠端伺服器。 *remoteserver*是**sysname**，預設值是 Null。 如果未指定*remoteserver* ，則會傳回本機伺服器上定義之所有遠端伺服器的相關資訊。  
  
 [ @remotename **=** ] **'***remote_name***'**  
 這是遠端伺服器上的特定遠端登入。 *remote_name*是**sysname**，預設值是 Null。 如果未指定*remote_name* ，就會傳回針對*remoteserver*定義之所有遠端使用者的相關資訊。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|伺服器|**sysname**|本機伺服器上定義之遠端伺服器的名稱。|  
|local_user_name|**sysname**|來自伺服器的遠端登入所對應之本機伺服器的登入。|  
|remote_user_name|**sysname**|對應至 local_user_name 的遠端伺服器登入。|  
|選項|**sysname**|信任 = 從遠端伺服器連接到本機伺服器時，遠端登入無需提供密碼。<br /><br /> 未受信任 (或空白) = 從遠端伺服器連接到本機伺服器時，會提示遠端登入輸入密碼。|  
  
## <a name="remarks"></a>備註  
 請使用 sp_helpserver 列出本機伺服器上所定義的遠端伺服器名稱。  
  
## <a name="permissions"></a>權限  
 不檢查任何權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-reporting-help-on-a-single-server"></a>A. 報告單一伺服器的說明  
 下列範例會顯示遠端伺服器 `Accounts` 上所有遠端使用者的相關資訊。  
  
```  
EXEC sp_helpremotelogin 'Accounts';  
```  
  
### <a name="b-reporting-help-on-all-remote-users"></a>B. 報告所有遠端使用者的說明  
 下列範例會顯示本機伺服器所知的所有遠端伺服器之所有遠端使用者的相關資訊。  
  
```  
EXEC sp_helpremotelogin;  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_addremotelogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addremotelogin-transact-sql.md)   
 [sp_dropremotelogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropremotelogin-transact-sql.md)   
 [sp_helpserver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [sp_remoteoption &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-remoteoption-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

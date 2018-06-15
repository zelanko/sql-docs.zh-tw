---
title: sp_changereplicationserverpasswords (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_changereplicationserverpasswords_TSQL
- sp_changereplicationserverpasswords
helpviewer_keywords:
- sp_changereplicationserverpasswords
ms.assetid: 9333da96-3a1c-4adb-9a74-5dac9ce596df
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 7c27142aa0e628e7041202429ae6bbaee0b87a1f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32989693"
---
# <a name="spchangereplicationserverpasswords-transact-sql"></a>sp_changereplicationserverpasswords (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  變更儲存的密碼[!INCLUDE[msCoName](../../includes/msconame-md.md)]Windows 帳戶或[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]連接到複寫拓撲中的伺服器時，複寫代理程式所使用的登入。 通常您必須變更在伺服器執行的每個個別代理程式的密碼，即使它們都使用相同的登入或帳戶也不例外。 這個預存程序可讓您變更所有在伺服器執行的複寫代理程式所用的給定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入或 Windows 帳戶之所有執行個體的密碼。 這個預存程序執行於 master 資料庫複寫拓撲中的任何一部伺服器。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_changereplicationserverpasswords [ @login_type = ] login_type  
        , [ @login = ] 'login'   
        , [ @password = ] 'password'  
    [ , [ @server = ] 'server' ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@login_type** =] *login_type*  
 這是所提供之認證的驗證類型。 *login_type*是**tinyint**，沒有預設值。  
  
 **1** = Windows 整合式的驗證  
  
 **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證  
  
 [ **@login** =] **'***登入***'**  
 這是您要變更的 Windows 帳戶或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入的名稱。 *登入*是**nvarchar （257)**，沒有預設值  
  
 [ **@password** =] **'***密碼***'**  
 要儲存的新密碼指定*登入*。 *密碼*是**sysname**，沒有預設值。  
  
> [!NOTE]  
>  在變更複寫密碼之後，必須停止並重新啟動使用該代理程式變更生效前所用密碼的每一個代理程式。  
  
 [ **@server** =] **'***伺服器***'**  
 這是要變更儲存密碼的伺服器連接。 *伺服器*是**sysname**，而且可以是下列值之一：  
  
|Value|Description|  
|-----------|-----------------|  
|**散發者**|所有與散發者的代理程式連接。|  
|**發行者**|所有與發行者的代理程式連接。|  
|**訂閱者**|所有與訂閱者的代理程式連接。|  
|**%** （預設值）|所有與複寫拓撲中所有伺服器的代理程式連接。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_changereplicationserverpasswords**用於所有複寫類型。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色可以執行**sp_changereplicationserverpasswords**。  
  
## <a name="see-also"></a>另請參閱  
 [檢視及修改複寫安全性設定](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)  
  
  

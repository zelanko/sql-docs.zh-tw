---
title: sp_dropserver （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 09/07/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dropserver_TSQL
- sp_dropserver
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dropserver
ms.assetid: 0fc83e35-0caa-49a3-a4b6-a1890d4f46ef
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 0155b154a1d63343c157bc2eca6e5cbd7c1b8968
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68124831"
---
# <a name="sp_dropserver-transact-sql"></a>sp_dropserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 本機執行個體上的已知遠端和連結伺服器清單中移除伺服器。  
  
 ![連結圖示](../../database-engine/configure-windows/media/topic-link.gif "連結圖示") [transact-sql 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql  
sp_dropserver [ @server = ] 'server'   
     [ , [ @droplogins = ] { 'droplogins' | NULL} ]  
```  
  
## <a name="arguments"></a>引數  
 *伺服器*  
 這是要移除的伺服器。 *伺服器*是**sysname**，沒有預設值。 *伺服器*必須存在。  
  
 *droplogins*  
 表示如果指定**droplogins** ，則也必須移除*伺服器*相關的遠端和連結伺服器登入。 **`@droplogins`** 是**char （10）**，預設值是 Null。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 如果您在具有相關聯遠端和連結伺服器登入專案的伺服器上執行**sp_dropserver** ，或已設定為複寫發行者，則會傳回錯誤訊息。 當您移除伺服器時，若要移除伺服器的所有遠端和連結伺服器登入，請使用**droplogins**引數。  
  
 **sp_dropserver**不能在使用者自訂交易內執行。  
  
## <a name="permissions"></a>權限  
 需要伺服器的 ALTER ANY LINKED SERVER 權限。  
  
## <a name="examples"></a>範例  
 下列範例會從 `ACCOUNTS` 本機執行個體移除遠端伺服器 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和所有相關聯的遠端登入。  
  
```  
sp_dropserver 'ACCOUNTS', 'droplogins';  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的安全性預存程式](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addserver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [sp_dropremotelogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropremotelogin-transact-sql.md)   
 [sp_helpremotelogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpremotelogin-transact-sql.md)   
 [sp_helpserver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

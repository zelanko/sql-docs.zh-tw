---
title: sp_changesubscriptiondtsinfo (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
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
- sp_changesubscriptiondtsinfo
- sp_changesubscriptiondtsinfo_TSQL
helpviewer_keywords:
- sp_changesubscriptiondtsinfo
ms.assetid: 64fc085f-f81b-493b-b59a-ee6192d9736d
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c6f1998ee847522f1237a55f5b6174861b774d69
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="spchangesubscriptiondtsinfo-transact-sql"></a>sp_changesubscriptiondtsinfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  變更訂閱的 Data Transformation Services (DTS) 封裝屬性。 這個預存程序執行於訂閱資料庫的訂閱者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_changesubscriptiondtsinfo [ [ @job_id = ] job_id ]  
    [ , [ @dts_package_name= ] 'dts_package_name' ]  
    [ , [ @dts_package_password= ] 'dts_package_password' ]  
    [ , [ @dts_package_location= ] 'dts_package_location' ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@job_id=**] *job_id*  
 這是發送訂閱之散發代理程式的作業識別碼。 *job_id*是**varbinary （16)**，沒有預設值。 若要尋找散發作業識別碼，請執行**sp_helpsubscription**或**sp_helppullsubscription**。  
  
 [ **@dts_package_name**=] **'***dts_package_name***'**  
 指定 DTS 封裝的名稱。 *dts_package_name*是**sysname**，預設值是 NULL。 例如，若要指定封裝名**DTSPub_Package**，您會指定`@dts_package_name = N'DTSPub_Package'`。  
  
 [ **@dts_package_password**=] **'***dts_package_password***'**  
 指定封裝的密碼。 *dts_package_password*是**sysname**預設值是 NULL，其指定密碼屬性維持不變。  
  
> [!NOTE]  
>  DTS 封裝必須有密碼。  
  
 [ **@dts_package_location**=] **'***dts_package_location***'**  
 指定封裝的位置。 *dts_package_location*是**nvarchar （12)**，預設值是 NULL，指定封裝位置是維持不變。 封裝的位置可以變更為**散發者**或**訂閱者**。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_changesubscriptiondtsinfo**用於快照式複寫和異動複寫是只有發送訂閱的。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定伺服器角色、 **db_owner**固定的資料庫角色或訂閱的建立者可以執行**sp_changesubscriptiondtsinfo**。  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

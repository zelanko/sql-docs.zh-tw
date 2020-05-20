---
title: sp_changesubscriptiondtsinfo （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changesubscriptiondtsinfo
- sp_changesubscriptiondtsinfo_TSQL
helpviewer_keywords:
- sp_changesubscriptiondtsinfo
ms.assetid: 64fc085f-f81b-493b-b59a-ee6192d9736d
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: fd0d08a045f67b436bd732b01a2279c923fc9461
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82824068"
---
# <a name="sp_changesubscriptiondtsinfo-transact-sql"></a>sp_changesubscriptiondtsinfo (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

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
`[ @job_id = ] job_id`這是發送訂閱之散發代理程式的作業識別碼。 *job_id*是**Varbinary （16）**，沒有預設值。 若要尋找發佈作業識別碼，請執行**sp_helpsubscription**或**sp_helppullsubscription**。  
  
`[ @dts_package_name = ] 'dts_package_name'`指定 DTS 封裝的名稱。 *dts_package_name*是**sysname**，預設值是 Null。 例如，若要指定名為**DTSPub_Package**的封裝，您可以指定 `@dts_package_name = N'DTSPub_Package'` 。  
  
`[ @dts_package_password = ] 'dts_package_password'`指定封裝上的密碼。 *dts_package_password*是**sysname** ，預設值是 Null，它會指定 password 屬性保持不變。  
  
> [!NOTE]  
>  DTS 封裝必須有密碼。  
  
`[ @dts_package_location = ] 'dts_package_location'`指定封裝位置。 *dts_package_location*是**Nvarchar （12）**，預設值是 Null，指定封裝位置保持不變。 封裝的位置可以**變更為「** 散發者」或「**訂閱者**」。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_changesubscriptiondtsinfo**用於僅限發送訂閱的快照式複寫和異動複寫。  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色的成員、 **db_owner**固定資料庫角色或訂閱的建立者，才能夠執行**sp_changesubscriptiondtsinfo**。  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

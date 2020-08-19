---
description: sp_helpxactsetjob (Transact-SQL)
title: sp_helpxactsetjob (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpxactsetjob
- sp_helpxactsetjob_TSQL
helpviewer_keywords:
- sp_helpxactsetjob
ms.assetid: 242cea3e-e6ac-4f84-a072-b003b920eb33
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 60d17af686d0ff289589d09dff0177b9696f17a4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88446968"
---
# <a name="sp_helpxactsetjob-transact-sql"></a>sp_helpxactsetjob (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  顯示 Oracle 發行者的 Xactset 作業的相關資訊。 這個預存程序執行於任何資料庫中的散發者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helpxactsetjob [ @publisher = ] 'publisher'   
```  
  
## <a name="arguments"></a>引數  
`[ @publisher = ] 'publisher'`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]這是作業所屬的非發行者名稱。 *publisher* 是 **sysname**，沒有預設值。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**jobnumber**|**int**|Oracle 作業編號。|  
|**lastdate**|**Varchar (22) **|上次作業執行的日期。|  
|**thisdate**|**Varchar (22) **|變更的時間|  
|**nextdate**|**Varchar (22) **|下次作業執行的日期。|  
|**broken**|**varchar(1)**|指出作業是否中斷的旗標。|  
|**區間**|**Varchar (200) **|作業的間隔時間。|  
|**失敗**|**int**|作業的失敗次數。|  
|**xactsetjobwhat**|**Varchar (200) **|作業所執行的程序名稱。|  
|**xactsetjob**|**varchar(1)**|作業的狀態，它可以是下列項目之一：<br /><br /> **1** -作業已啟用。<br /><br /> **0** -作業已停用。|  
|**xactsetlonginterval**|**int**|作業的長間隔時間。|  
|**xactsetlongthreshold**|**int**|作業的長臨界值。|  
|**xactsetshortinterval**|**int**|作業的短間隔時間。|  
|**xactsetshortthreshold**|**int**|作業的短臨界值。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_helpxactsetjob** 用於 Oracle 發行者的快照式複寫和異動複寫中。  
  
 **sp_helpxactsetjob** 一律會傳回「發行者」端的 Xactset 作業 (HREPL_XactSetJob) 的目前設定。 如果 Xactset 作業目前在作業佇列中，還會另外從以 Oracle 發行者管理員帳戶建立的 USER_JOB 資料字典檢視，傳回作業屬性。  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色的成員，才可以執行 **sp_helpxactsetjob**。  
  
## <a name="see-also"></a>另請參閱  
 [設定 Oracle 發行者的交易集作業 &#40;複寫 Transact-SQL 程式設計&#41;](../../relational-databases/replication/administration/configure-the-transaction-set-job-for-an-oracle-publisher.md)   
 [sp_publisherproperty &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md)  
  
  

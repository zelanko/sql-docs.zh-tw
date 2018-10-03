---
title: sp_monitor & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_monitor_TSQL
- sp_monitor
dev_langs:
- TSQL
helpviewer_keywords:
- sp_monitor
ms.assetid: cb628496-2f9b-40e4-b018-d0831c4cb018
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5312413386dae9915b9ac6649b4210541d45b1db
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47644426"
---
# <a name="spmonitor-transact-sql"></a>sp_monitor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  顯示相關的統計資料[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_monitor  
```  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|描述|  
|-----------------|-----------------|  
|**last_run**|時間**sp_monitor**上次執行。|  
|**current_run**|時間**sp_monitor**正在執行。|  
|**seconds**|之後經過的秒數字**sp_monitor**執行。|  
|**cpu_busy**|伺服器電腦的 CPU 已執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 工作的秒數。|  
|**io_busy**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已花在處理輸入和輸出作業的秒數。|  
|**閒置**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已閒置的秒數。|  
|**packets_received**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已讀取的輸入封包數。|  
|**packets_sent**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已寫入的輸出封包數。|  
|**packet_errors**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在讀取和寫入封包時所發現的錯誤數。|  
|**total_read**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的讀取數。|  
|**total_write**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的寫入數。|  
|**total_errors**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在讀取和寫入時所發現的錯誤數。|  
|**連線**|登入或嘗試登入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的次數。|  
  
## <a name="remarks"></a>備註  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會透過一系列的函數來持續追蹤它已完成的工作量。 執行**sp_monitor**會顯示這些函式所傳回的目前值，並顯示多少上次執行此程序以來已經變更。  
  
 每個資料行，在表單中列印統計資料*數字*(*數目*)-*號碼*%或*數目*(*數目*). 第一個*數字*指的秒數 (如**cpu_busy**， **io_busy**，和**閒置**) 或總數 （針對其他變數） 因為[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]已重新啟動。 *數字*括號括住參考的秒數或總數自從上次**sp_monitor**執行。 百分比是開始的時間百分比**sp_monitor**上次執行。 例如，如果此報表會顯示**cpu_busy**是 4250 （215)-68%，CPU 已忙碌 4250 秒[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]上次啟動，215 秒**sp_monitor**是上次執行 和 68%總時間，因為**sp_monitor**上次執行。  
  
## <a name="permissions"></a>Permissions  
 需要 **系統管理員 (sysadmin)** 固定伺服器角色中的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會報告有關 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 忙碌情形的資訊。  
  
```  
USE master  
EXEC sp_monitor  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
||||  
|-|-|-|  
|**last_run**|**current_run**|**seconds**|  
|Mar 29 1998 11:55AM|Apr 4 1998 2:22 PM|561|  
  
||||  
|-|-|-|  
|**cpu_busy**|**io_busy**|**閒置**|  
|190(0)-0%|187(0)-0%|148(556)-99%|  
  
||||  
|-|-|-|  
|**packets_received**|**packets_sent**|**packet_errors**|  
|16(1)|20(2)|0(0)|  
  
|||||  
|-|-|-|-|  
|**total_read**|**total_write**|**total_errors**|**連線**|  
|141(0)|54920(127)|0(0)|4(0)|  
  
## <a name="see-also"></a>另請參閱  
 [sp_who &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

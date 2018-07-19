---
title: sp_copysubscription (TRANSACT-SQL) |Microsoft 文件
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
- sp_copysubscription
- sp_copysubscription_TSQL
helpviewer_keywords:
- sp_copysubscription
ms.assetid: 3c56cd62-2966-4e87-a986-44cb3fd0b760
caps.latest.revision: 33
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 3cae06562e37cf10c2fa94934eedb20880b4391a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32993215"
---
# <a name="spcopysubscription-transact-sql"></a>sp_copysubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

    
> [!IMPORTANT]  
>  可附加訂閱功能已被取代，未來的版本將會移除它。 這項功能不應該使用在新的開發工作中。 對於使用參數化篩選來進行資料分割的合併式發行集，我們建議您使用資料分割快照集的新功能，這些功能可以簡化大量訂閱的初始化。 如需詳細資訊，請參閱＜ [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)＞。 對於未進行資料分割的發行集，您可以用備份來初始化訂閱。 如需詳細資訊，請參閱 [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)中手動初始化訂閱。  
  
 複製有提取訂閱但沒有發送訂閱的訂閱資料庫。 只能複製單一檔案資料庫。 這個預存程序執行於訂閱資料庫的訂閱者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_copysubscription [ @filename = ] 'file_name'  
    [ , [ @temp_dir = ] 'temp_dir' ]  
    [ , [ @overwrite_existing_file = ] overwrite_existing_file]  
```  
  
## <a name="arguments"></a>引數  
 [ **@filename =**] **'***file_name***'**  
 這是指定用來儲存資料檔 (.mdf) 複本的完整路徑 (包括檔案名稱) 之字串。 *檔案名稱*是**nvarchar （260)**，沒有預設值。  
  
 [  **@temp_dir=**] **'***temp_dir***'**  
 這是包含暫存檔之目錄的名稱。 *temp_dir*是**nvarchar （260)**，預設值是 NULL。 如果是 NULL， [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]將使用預設資料目錄。 目錄應該有足夠的空間來存放組合了所有訂閱者資料庫檔案的檔案大小。  
  
 [  **@overwrite_existing_file=**] **'***overwrite_existing_file***'**  
 是選擇性的布林值旗標，指定是否要覆寫現有的檔案中指定的相同名稱的**@filename**。 *overwrite_existing_file*是**元**，預設值是**0**。 如果**1**，它會覆寫所指定的檔案**@filename**，如果它存在。 如果**0**，預存程序失敗時，如果檔案存在，而且不會覆寫檔案。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_copysubscription**用於所有類型的複寫訂閱資料庫複製到檔案，做為套用在訂閱者的快照集替代。 資料庫必須設定成只支援提取訂閱。 有適當權限的使用者可以建立訂閱資料庫的副本，再複製、傳輸或利用電子郵件來傳送訂閱檔 (.msf) 到另一個訂閱者，之後，便能在此將它附加成一項訂閱。  
  
 所複製的訂閱資料庫大小必須小於 2 GB。  
  
 **sp_copysubscription**只支援具有客訂閱的資料庫，當資料庫有伺服器訂閱時無法執行。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色可以執行**sp_copysubscription**。  
  
## <a name="see-also"></a>另請參閱  
 [替代快照集資料夾位置](../../relational-databases/replication/alternate-snapshot-folder-locations.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

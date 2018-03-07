---
title: "RESTORE REWINDONLY (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- RESTORE_REWINDONLY_TSQL
- RESTORE REWINDONLY
dev_langs:
- TSQL
helpviewer_keywords:
- closing backup devices
- backup devices [SQL Server], rewinding
- media [SQL Server]
- open back devices
- rewinding backup devices
- RESTORE REWINDONLY statement
ms.assetid: 7f825b40-2264-4608-9809-590d0f09d882
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bf67d54e58f08296878c0781158e7b878b0b2a49
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="restore-statements---rewindonly-transact-sql"></a>RESTORE 陳述式-REWINDONLY (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  倒轉和關閉設定 NOREWIND 選項來執行的 BACKUP 或 RESTORE 陳述式保留了其開啟狀態的指定磁帶裝置。 這個命令只適用於磁帶裝置。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
RESTORE REWINDONLY   
FROM <backup_device> [ ,...n ]  
[ WITH {UNLOAD | NOUNLOAD}]  
}   
[;]  
  
<backup_device> ::=  
{   
   { logical_backup_device_name |  
      @logical_backup_device_name_var }  
   | TAPE = { 'physical_backup_device_name' |  
       @physical_backup_device_name_var }   
}   
```  
  
## <a name="arguments"></a>引數  
 **\<backup_device> ::=** 
  
 指定還原作業要用的邏輯或實體備份裝置。  
  
 { *logical_backup_device_name* | **@ * * * logical_backup_device_name_var* } 的邏輯名稱，它必須遵照識別碼規則，備份裝置由**sp_addumpdevice**從還原資料庫。如果提供的變數 (**@***logical_backup_device_name_var*)，可用的備份裝置名稱指定為字串常數 (**@ * * * logical_backup_device_name_var*  =  *logical_backup_device_name*) 或指定為字元字串資料型別變數除了**ntext**或**文字**資料型別。  
  
 {磁碟 |磁帶}  **=**  { **'***physical_backup_device_name***'** | **@ * * * physical_backup_device_name_var* } 可讓您從具名的磁碟或磁帶裝置還原備份。應該用裝置的實際名稱 （例如，完整路徑和檔案名稱） 指定磁碟和磁帶的裝置類型： 磁碟 = 'C:\Program Files\Microsoft SQL Server\MSSQL\BACKUP\Mybackup.bak' 或 TAPE ='\\\\。 \TAPE0'。如果指定為變數 (**@***physical_backup_device_name_var*)，可用的裝置名稱指定為字串常數 (**@ * * * physical_backup_device_name_var* = '*physcial_backup_device_name *') 或指定為字元字串資料型別變數除了**ntext**或**文字**資料型別。  
  
 如果所用的網路伺服器是用 UNC 名稱 (必須包含機器名稱)，請指定磁碟裝置類型。 如需有關使用 UNC 名稱的詳細資訊，請參閱[備份裝置 &#40;SQL Server &#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md).  
  
 執行 Microsoft SQL Server 的帳戶必須有讀取權限的遠端電腦或網路伺服器，才能執行還原作業。  
  
 *n*  
 這是一個預留位置，表示可以指定多個備份裝置和邏輯備份裝置。 備份裝置或邏輯備份裝置數目上限是**64**。  
  
 還原序列所需要的備份裝置數目，是否與建立備份所屬的媒體集時所用的備份裝置數目相同，取決於還原作業是離線或在線上進行。 如果是離線還原，用來還原備份的裝置可以比建立備份時所用的裝置少。 線上還原需要備份的所有備份裝置。 試圖用較少的裝置來還原會失敗。  
  
 如需詳細資訊，請參閱 [備份裝置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)執行個體上建立資料庫備份，就需要這個選項。  
  
> [!NOTE]  
>  當從鏡像媒體集中還原備份時，每個媒體家族只能指定單一鏡像。 不過，如果有其他鏡像，當出現錯誤時，解決部份還原問題的速度會比較快。 您可以利用另一個鏡像的對應磁碟區來替代損毀的媒體磁碟區。 請注意，如果是離線還原，您可以從比媒體家族少的裝置進行還原，但每個家族只會處理一次。  
  
 **使用選項**  
  
 UNLOAD  
 指定 RESTORE 完成之後，便自動倒轉和卸載磁帶。 依預設，當啟動新使用者工作階段時，會設定 UNLOAD。 這項設定會維持到指定 NOUNLOAD 為止。 這個選項只適用於磁帶裝置。 如果 RESTORE 使用非磁帶裝置，便會忽略這個選項。  
  
 NOUNLOAD  
 指定在 RESTORE 之後，不自動卸載磁帶機中的磁帶。 NOUNLOAD 設定會維持到指定 UNLOAD 為止。  
  
 指定在 RESTORE 之後，不自動卸載磁帶機中的磁帶。 NOUNLOAD 設定會維持到指定 UNLOAD 為止。  
  
## <a name="general-remarks"></a>一般備註  
 RESTORE REWINDONLY 是替代 RESTORE LABELONLY FROM TAPE =\<名稱 > WITH REWIND。 您可以取得一份開啟的磁帶機，分別從[sys.dm_io_backup_tapes](../../relational-databases/system-dynamic-management-views/sys-dm-io-backup-tapes-transact-sql.md)動態管理檢視。  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>Permissions  
 任何使用者都可以使用 RESTORE REWINDONLY。  
  
## <a name="see-also"></a>另請參閱  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [媒體集、媒體家族與備份組 &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [備份記錄與標頭資訊 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)  
  
  


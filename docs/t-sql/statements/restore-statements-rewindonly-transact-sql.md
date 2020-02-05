---
title: RESTORE REWINDONLY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 0b70fdfc02e876310841bde3646aab9620c56951
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "68082500"
---
# <a name="restore-statements---rewindonly-transact-sql"></a>RESTORE 陳述式 - REWINDONLY (Transact-SQL)
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
  
 { *logical_backup_device_name* |  **@** _logical\_backup\_device\_name\_var_ }  
 這是用來還原資料庫的 **sp_addumpdevice** 所建立之備份裝置的邏輯名稱，它必須遵循識別碼的規則。 如果備份裝置名稱是以變數 ( **@** _logical\_backup\_device\_name\_var_) 的方式來提供，您可以將此名稱指定為字串常數 ( **@** _logical\_backup\_device\_name\_var_ = _logical\_backup\_device\_name_)，或指定為字元字串資料類型的變數，但 **ntext** 或 **text** 資料類型除外。  
  
 {DISK | TAPE } **=** { **'** _physical\_backup\_device\_name_ **'**  |  **@** _physical\_backup\_device\_name\_var_ }  
 可讓您從指定的磁碟或磁帶裝置中還原備份。 您應該用裝置的實際名稱 (如完整路徑和檔案名稱) 來指定磁碟和磁帶的裝置類型：DISK = 'C:\Program Files\Microsoft SQL Server\MSSQL\BACKUP\Mybackup.bak' 或 TAPE = '\\\\.\TAPE0'。 如果裝置名稱是以變數 ( **@** _physical\_backup\_device\_name\_var_) 的方式來提供，您可以將此裝置名稱指定為字串常數 ( **@** _physical\_backup\_device\_name\_var_ = '*physical_backup_device_name*')，或指定為字元字串資料類型的變數，但 **ntext** 或 **text** 資料類型除外。  
  
 如果所用的網路伺服器是用 UNC 名稱 (必須包含機器名稱)，請指定磁碟裝置類型。 如需如何使用通用命名慣例 (UNC) 名稱的詳細資訊，請參閱[備份裝置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)。  
  
 您用來執行 Microsoft SQL Server 的帳戶，必須有遠端電腦或網路伺服器的 READ 存取權，才能執行 RESTORE 作業。  
  
 *n*  
 這是一個預留位置，表示可以指定多個備份裝置和邏輯備份裝置。 備份裝置或邏輯備份裝置的最大數目是 **64**。  
  
 還原序列所需要的備份裝置數目，是否與建立備份所屬的媒體集時所用的備份裝置數目相同，取決於還原作業是離線或在線上進行。 如果是離線還原，用來還原備份的裝置可以比建立備份時所用的裝置少。 線上還原需要備份的所有備份裝置。 試圖用較少的裝置來還原會失敗。  
  
 如需詳細資訊，請參閱 [備份裝置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)執行個體上建立資料庫備份，就需要這個選項。  
  
> [!NOTE]  
>  當從鏡像媒體集中還原備份時，每個媒體家族只能指定單一鏡像。 不過，如果有其他鏡像，當出現錯誤時，解決部份還原問題的速度會比較快。 您可以利用另一個鏡像的對應磁碟區來替代損毀的媒體磁碟區。 請注意，如果是離線還原，您可以從比媒體家族少的裝置進行還原，但每個家族只會處理一次。  
  
 **WITH 選項**  
  
 UNLOAD  
 指定 RESTORE 完成之後，便自動倒轉和卸載磁帶。 依預設，當啟動新使用者工作階段時，會設定 UNLOAD。 這項設定會維持到指定 NOUNLOAD 為止。 這個選項只適用於磁帶裝置。 如果 RESTORE 使用非磁帶裝置，便會忽略這個選項。  
  
 NOUNLOAD  
 指定在 RESTORE 之後，不自動卸載磁帶機中的磁帶。 NOUNLOAD 設定會維持到指定 UNLOAD 為止。  
  
## <a name="general-remarks"></a>一般備註  
 RESTORE REWINDONLY 可用來取代 RESTORE LABELONLY FROM TAPE = \<name> WITH REWIND。 您可以從 [sys.dm_io_backup_tapes](../../relational-databases/system-dynamic-management-views/sys-dm-io-backup-tapes-transact-sql.md) 動態管理檢視中取得開啟的磁帶機清單。  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>權限  
 任何使用者都可以使用 RESTORE REWINDONLY。  
  
## <a name="see-also"></a>另請參閱  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [媒體集、媒體家族與備份組 &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [備份記錄與標頭資訊 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)  
  
  


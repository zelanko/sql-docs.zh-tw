---
title: sp_addumpdevice (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_addumpdevice_TSQL
- sp_addumpdevice
dev_langs:
- TSQL
helpviewer_keywords:
- backup devices [SQL Server], defining
- sp_addumpdevice
ms.assetid: c2d2ae49-0808-46d8-8444-db69a69d0ec3
caps.latest.revision: 49
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 63b5f8f4f80bbb02db1267aec0a1fa2710ee294a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="spaddumpdevice-transact-sql"></a>sp_addumpdevice (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  
**適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [目前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658))。  

將備份裝置加入至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_addumpdevice [ @devtype = ] 'device_type'   
    , [ @logicalname = ] 'logical_name'   
    , [ @physicalname = ] 'physical_name'  
      [ , { [ @cntrltype = ] controller_type |  
          [ @devstatus = ] 'device_status' }  
      ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@devtype=** ] **'***device_type***'**  
 這是備份裝置的類型。 *device_type*是**varchar （20)**，沒有預設值，它可以是下列值之一。  
  
|Value|Description|  
|-----------|-----------------|  
|**disk**|做為備份裝置的硬碟檔。|  
|**磁帶**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 所支援的任何磁帶裝置。<br /><br /> 注意：未來的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本中將會移除磁帶備份裝置的支援。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。|  
  
 [ **@logicalname =** ] **'***logical_name***'**  
 這是 BACKUP 和 RESTORE 陳述式所用之備份裝置的邏輯名稱。 *logical_name*是**sysname**，沒有預設值，不能是 NULL。  
  
 [ **@physicalname =** ] **'***physical_name***'**  
 這是備份裝置的實體名稱。 實體名稱必須遵照作業系統檔案名稱或網路裝置通用命名慣例的規則，且必須包括完整路徑。 *physical_name*是**nvarchar （260)**，沒有預設值的值，而且不能是 NULL。  
  
 當在遠端網路位置建立備份裝置時，請確定用來啟動 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的名稱有遠端電腦的適當寫入功能。  
  
 如果您加入磁帶裝置時，這個參數必須是由 Windows; 指派給本機磁帶裝置，實體名稱例如，  **\\ \\。 \TAPE0**第一個磁帶裝置的電腦上。 磁帶裝置必須連接到伺服器電腦，不能在遠端使用。 請用引號括住包含非英數字元的名稱。  
  
> [!NOTE]  
>  此程序將指定的實體名稱輸入目錄中。 此程序不會試著存取或建立裝置。  
  
 [ **@cntrltype =** ] **'***controller_type***'**  
 已過時。 若指定，則會忽略此參數。 支援這個項目的目的，只是為了與舊版相容。 初次使用**sp_addumpdevice**應該省略此參數。  
  
 [ **@devstatus =** ] **'***device_status***'**  
 已過時。 若指定，則會忽略此參數。 支援這個項目的目的，只是為了與舊版相容。 初次使用**sp_addumpdevice**應該省略此參數。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 無  
  
## <a name="remarks"></a>備註  
 **sp_addumpdevice**新增到備份裝置**sys.backup_devices**目錄檢視。 可在 BACKUP 和 RESTORE 陳述式中以邏輯方式參照裝置。 **sp_addumpdevice**不會執行任何存取權的實體裝置。 只有在執行 BACKUP 或 RESTORE 陳述式時，才對指定的裝置進行存取。 建立邏輯備份裝置可簡化 BACKUP 和 RESTORE 陳述式，其中指定裝置名稱是使用 "TAPE =" 或 "DISK =" 子句指定裝置路徑的替代方法。  
  
 擁有權和權限問題可能會干擾磁碟或檔案備份裝置的使用。 請確定用來啟動 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的 Windows 帳戶已取得適當的檔案權限。  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 支援利用 Windows 支援的磁帶裝置來進行磁帶備份。 如需有關 Windows 所支援之磁帶裝置的詳細資訊，請參閱 Windows 的硬體相容性清單。 若要檢視電腦中所能使用的磁帶裝置，請使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
 請只用磁帶機製造商所建議的特定磁帶機專用磁帶。 如果您使用數位錄音機 (DAT)，請使用電腦等級的 DAT 磁帶 (數位資料儲存媒體 (DDS))。  
  
 **sp_addumpdevice**無法在交易內執行。  
  
 若要刪除裝置，請使用[sp_dropdevice](../../relational-databases/system-stored-procedures/sp-dropdevice-transact-sql.md)或[SQL Server Management Studio](../../relational-databases/backup-restore/delete-a-backup-device-sql-server.md)。  
  
## <a name="permissions"></a>Permissions  
 需要 **diskadmin** 固定伺服器角色的成員資格。  
  
 需要寫入磁碟的權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-adding-a-disk-dump-device"></a>A. 加入磁碟傾印裝置  
 下列範例會加入名稱為 `mydiskdump` 的磁碟備份裝置，實體名稱是 `c:\dump\dump1.bak`。  
  
```  
USE master;  
GO  
EXEC sp_addumpdevice 'disk', 'mydiskdump', 'c:\dump\dump1.bak';  
```  
  
### <a name="b-adding-a-network-disk-backup-device"></a>B. 加入網路磁碟備份裝置  
 下列範例會顯示如何加入稱為 `networkdevice` 的遠端磁碟備份裝置。 用來啟動 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的名稱必須有該遠端檔案 (`\\<servername>\<sharename>\<path>\<filename>.bak`) 的權限。  
  
```  
USE master;  
GO  
EXEC sp_addumpdevice 'disk', 'networkdevice',  
    '\\<servername>\<sharename>\<path>\<filename>.bak';  
```  
  
### <a name="c-adding-a-tape-backup-device"></a>C. 加入磁帶備份裝置  
 下列範例會加入實體名稱為 `tapedump1` 的 `\\.\tape0` 裝置。  
  
```  
USE master;  
GO  
EXEC sp_addumpdevice 'tape', 'tapedump1', '\\.\tape0';  
```  
  
### <a name="d-backing-up-to-a-logical-backup-device"></a>D. 備份至邏輯備份裝置  
 下列範例會針對備份磁碟檔案建立邏輯備份裝置，即 `AdvWorksData`。 接著，這個範例會將 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫備份至這個邏輯備份裝置。  
  
```  
USE master;  
GO  
EXEC sp_addumpdevice 'disk', 'AdvWorksData',   
'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\BACKUP\AdvWorksData.bak';  
GO  
BACKUP DATABASE AdventureWorks2012   
 TO AdvWorksData  
   WITH FORMAT;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [備份裝置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [定義磁碟檔案的邏輯備份裝置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-disk-file-sql-server.md)   
 [定義磁帶機的邏輯備份裝置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [sp_dropdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdevice-transact-sql.md)   
 [sys.backup_devices &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-backup-devices-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

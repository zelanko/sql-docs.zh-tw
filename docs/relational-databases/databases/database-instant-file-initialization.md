---
title: 資料庫檔案立即初始化 | Microsoft 文件
ms.custom: ''
ms.date: 01/09/2018
ms.prod: sql
ms.prod_service: database-engine
ms.component: databases
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- initializing files [SQL Server]
- instant file initialization [SQL Server]
- fast file initialization [SQL Server]
- file initialization [SQL Server]
- IFI [SQL Server]
- database instant file initialization [SQL Server]
ms.assetid: 1ad468f5-4f75-480b-aac6-0b01b048bd67
caps.latest.revision: 33
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0f51ea699c269ddb237f4582d4f368dd76cdc149
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="database-file-initialization"></a>資料庫檔案初始化
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
系統會將資料和記錄檔初始化，以覆寫磁碟上先前刪除之檔案中所遺留的任何現有資料。 當您執行下列作業之一時，會先將資料檔和記錄檔清空 (填入 0)，藉以初始化檔案：  
  
- 建立資料庫。  
- 將資料或記錄檔新增至現有的資料庫。  
- 增加現有檔案的大小 (包括自動成長作業)。  
- 還原資料庫或檔案群組。  
  
檔案初始化會導致這些作業需要較長的時間。 不過，當資料第一次寫入檔案時，作業系統並不需要在檔案中填入 0。  
  
## <a name="instant-file-initialization-ifi"></a>檔案立即初始化 (IFI)  
在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，資料檔可以立即初始化，以避免清空作業。 檔案立即初始化可以加快先前提到的檔案作業執行速度。 立即檔案初始化會回收使用的磁碟空間，卻不會在該空間中填入零。 而是在新資料寫入檔案時將磁碟內容覆寫為新資料。 記錄檔無法立即初始化。  
  
> [!NOTE]  
> 檔案立即初始化只在 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[winxppro](../../includes/winxppro-md.md)] 或 [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] 或更新版本中提供。  

> [!IMPORTANT]
> 只有在資料檔中才能使用檔案立即初始化。 記錄檔在建立或增加大小時，一律會將檔案清空。
  
只有在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務啟動帳戶被授與 *SE_MANAGE_VOLUME_NAME* 時，才能使用檔案立即初始化。 Windows Administrator 群組的成員擁有此權限，並可將此權限授與其他使用者 (方法是將他們新增到「執行磁碟區維護工作」  安全性原則。  
  
> [!IMPORTANT]
> 使用[透明資料加密 (TDE)](../../relational-databases/security/encryption/transparent-data-encryption.md) 等某些功能時，會防止檔案立即初始化。  
  
授與帳戶「 `Perform volume maintenance tasks` 」權限：  
  
1.  在即將建立備份檔案的電腦上，開啟 [本機安全性原則] 應用程式 (`secpol.msc`)。  
  
2.  在左窗格中，展開 [本機原則] ，然後按一下 [使用者權限指派] 。  
  
3.  在右窗格中，按兩下 [執行磁碟區維護工作]。  
  
4.  按一下 [新增使用者或群組]  ，新增用於備份的任何使用者帳戶。  
  
5.  按一下 [套用] ，然後關閉所有 [本機安全性原則]  對話方塊。  

> [!NOTE]
> 從 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 開始，此權限可在安裝期間進行安裝時授與給服務帳戶。 如果使用[命令提示字元安裝](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)，請新增 /SQLSVCINSTANTFILEINIT 引數，或在[安裝精靈](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)中核取 [對 SQL Server Database Engine 服務授與「執行磁碟區維護工作」權限] 方塊。

> [!NOTE]
> 從 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP4 開始，以及 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，[sys.dm_server_services](../../relational-databases/system-dynamic-management-views/sys-dm-server-services-transact-sql.md) DMV 中的資料行 *instant_file_initialization_enabled* 可用來識別是否已啟用檔案立即初始化。

## <a name="remarks"></a>Remarks
如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務啟動帳戶被授與 *SE_MANAGE_VOLUME_NAME*，類似如下的告知性訊息會在啟動時記錄在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔： 

```
Database Instant File Initialization: enabled. For security and performance considerations see the topic 'Database Instant File Initialization' in SQL Server Books Online. This is an informational message only. No user action is required.
```

如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務啟動帳戶**未**被授與 *SE_MANAGE_VOLUME_NAME*，類似如下的告知性訊息會在啟動時記錄在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔： 

```
Database Instant File Initialization: disabled. For security and performance considerations see the topic 'Database Instant File Initialization' in SQL Server Books Online. This is an informational message only. No user action is required.
```

**適用於：** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (從 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP4 開始、[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 和 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)])

## <a name="security-considerations"></a>安全性考量  
在使用檔案立即初始化 (IFI) 時，由於刪除的磁碟內容只有在新資料寫入檔案時才會被覆寫；因此，直到其他資料寫入資料檔特定區域之前，未經授權的主體可能得以存取刪除的內容。 當資料庫檔案附加到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體之際，檔案上的判別存取控制清單 (DACL) 可降低此一資訊洩漏風險。 此 DACL 只允許 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶和本機系統管理員存取檔案。 但是，當檔案卸離後，沒有 *SE_MANAGE_VOLUME_NAME* 的使用者或服務便能存取該檔案。 在備份資料庫時，也會有類似的需要考量之處：如果備份檔案未使用適當的 DACL 保護，未經授權的使用者或服務便可存取刪除的內容。  

另一個考量是當檔案使用 IFI 增長時，SQL Server 系統管理員可能會存取原始頁面內容，並查看先前刪除的內容。

如果資料庫檔案裝載在存放區域網路上，則存放區域網路也可能會一律以預先初始化方式顯示新頁面，因此讓作業系統重新初始化頁面可能是不必要的額外負荷。
 
> [!NOTE]
> 此項建議的理由，是因為如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝在安全的實體環境中，啟用檔案立即初始化的效能優點會勝於安全性風險。
  
如果洩漏刪除的內容可能是一項隱憂，您應該採取下列其中一或兩個項動作：  
  
- 務必確保所有卸離的資料檔和備份檔都具有限制的 DACL。  
- 撤銷 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務啟動帳戶的 *SE_MANAGE_VOLUME_NAME*，可停用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的檔案立即初始化。 

> [!IMPORTANT]
> 停用檔案立即初始化，將會增加資料檔案的配置時間。  
  
> [!NOTE]  
> 停用立即檔案初始化只會影響使用者權限撤銷後建立或大小增加的檔案。  
  
## <a name="see-also"></a>另請參閱  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)  
  
  

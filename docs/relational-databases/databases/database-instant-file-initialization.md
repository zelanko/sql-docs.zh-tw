---
title: "資料庫檔案立即初始化 | Microsoft 文件"
ms.custom: 
ms.date: 11/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: databases
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- initializing files [SQL Server]
- instant file initialization [SQL Server]
- fast file initialization (SQL Server)
- file initialization [SQL Server]
- IFI [SQL Server]
ms.assetid: 1ad468f5-4f75-480b-aac6-0b01b048bd67
caps.latest.revision: "33"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 3f0ef2d2c733a0ab1f349d42d621303cc6c133a5
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2017
---
# <a name="database-file-initialization"></a>資料庫檔案初始化
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 系統會將資料和記錄檔初始化，以覆寫磁碟上先前刪除之檔案中所遺留的任何現有資料。 當您執行下列作業之一時，會先將資料檔和記錄檔清空 (填入 0)，藉以初始化檔案：  
  
- 建立資料庫。  
  
- 將資料或記錄檔新增至現有的資料庫。  
  
- 增加現有檔案的大小 (包括自動成長作業)。  
  
- 還原資料庫或檔案群組。  
  
檔案初始化會導致這些作業需要較長的時間。 不過，當資料第一次寫入檔案時，作業系統並不需要在檔案中填入 0。  
  
# <a name="instant-file-initialization-ifi"></a>檔案立即初始化 (IFI)  
在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，資料檔可以立即初始化，以避免清空作業。 檔案立即初始化可以加快先前提到的檔案作業執行速度。 立即檔案初始化會回收使用的磁碟空間，卻不會在該空間中填入零。 而是在新資料寫入檔案時將磁碟內容覆寫為新資料。 記錄檔無法立即初始化。  
  
> [!NOTE]  
>  檔案立即初始化只在 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[winxppro](../../includes/winxppro-md.md)] 或 [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] 或更新版本中提供。  

> [!IMPORTANT]
> 只有在資料檔中才能使用檔案立即初始化。 記錄檔在建立或增加大小時，一律會將檔案清空。
  
只有在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務啟動帳戶被授與 *SE_MANAGE_VOLUME_NAME* 時，才能使用檔案立即初始化。 Windows Administrator 群組的成員擁有此權限，並可將此權限授與其他使用者 (方法是將他們新增到「執行磁碟區維護工作」  安全性原則。  
  
使用[透明資料加密 (TDE)](../../relational-databases/security/encryption/transparent-data-encryption.md) 等某些功能時，會防止檔案立即初始化。  
  
授與帳戶「 `Perform volume maintenance tasks` 」權限：  
  
1.  在即將建立備份檔案的電腦上，開啟 [本機安全性原則] 應用程式 (`secpol.msc`)。  
  
2.  在左窗格中，展開 [本機原則] ，然後按一下 [使用者權限指派] 。  
  
3.  在右窗格中，按兩下 [執行磁碟區維護工作]。  
  
4.  按一下 [新增使用者或群組]  ，新增用於備份的任何使用者帳戶。  
  
5.  按一下 [套用] ，然後關閉所有 [本機安全性原則]  對話方塊。  
  
### <a name="security-considerations"></a>安全性考量  
 由於刪除的磁碟內容只有在新資料寫入檔案時才會被覆寫，因此，直到其他資料寫入資料檔特定區域之前，未經授權的主體可能得以存取刪除的內容。 當資料庫檔案附加到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體之際，檔案上的判別存取控制清單 (DACL) 可降低此一資訊洩漏風險。 此 DACL 只允許 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶和本機系統管理員存取檔案。 但是，當檔案卸離後，沒有 *SE_MANAGE_VOLUME_NAME* 的使用者或服務便能存取該檔案。 在備份資料庫時，也會有類似的需要考量之處：如果備份檔案未使用適當的 DACL 保護，未經授權的使用者或服務便可存取刪除的內容。  
 
 此項建議的理由，是因為如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝在安全環境中，啟用 IFI 的效能優點會勝於安全性風險。
  
 如果洩漏刪除的內容可能是一項隱憂，您應該採取下列其中一或兩個項動作：  
  
- 務必確保所有卸離的資料檔和備份檔都具有限制的 DACL。  
  
- 撤銷 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務啟動帳戶的 *SE_MANAGE_VOLUME_NAME*，可停用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的檔案立即初始化。  
  
> [!NOTE]  
> 停用立即檔案初始化只會影響使用者權限撤銷後建立或大小增加的檔案。  
  
## <a name="see-also"></a>另請參閱  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)  
  
  

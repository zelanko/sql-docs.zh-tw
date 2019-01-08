---
title: 資料庫檔案立即初始化 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- initializing files [SQL Server]
- instant file initializations [SQL Server]
- fast file initialization (SQL Server)
- file initialization [SQL Server]
ms.assetid: 1ad468f5-4f75-480b-aac6-0b01b048bd67
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 491c8a63c7ee3ed06c90356c58820f34ed3c0bf9
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52774270"
---
# <a name="database-instant-file-initialization"></a>資料庫立即檔案初始化
  系統會將資料和記錄檔初始化，以覆寫磁碟上先前刪除之檔案中所遺留的任何現有資料。 資料檔和記錄檔初始化的方式是先在您執行下列作業之一時，在檔案中填入 0：  
  
-   建立資料庫。  
  
-   新增檔案、記錄或資料到現有的資料庫。  
  
-   增加現有檔案的大小 (包括自動成長作業)。  
  
-   還原資料庫或檔案群組。  
  
 檔案初始化會導致這些作業需要較長的時間。 不過，當資料第一次寫入檔案時，作業系統並不需要在檔案中填入 0。  
  
## <a name="instant-file-initialization"></a>立即檔案初始化  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，資料檔可以立即初始化。 這可以加快先前提到之檔案作業的執行速度。 立即檔案初始化會回收使用的磁碟空間，卻不會在該空間中填入零。 而是在新資料寫入檔案時將磁碟內容覆寫為新資料。 記錄檔無法立即初始化。  
  
> [!NOTE]  
>  檔案立即初始化只在 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[winxppro](../../includes/winxppro-md.md)] 或 [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] 或更新版本中提供。  
  
 只有在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (MSSQLSERVER) 服務帳戶被授與 SE_MANAGE_VOLUME_NAME 時，才能使用立即檔案初始化。 Windows Administrator 群組的成員擁有此權限，並可將此權限授與其他使用者 (方法是將他們新增到「執行磁碟區維護工作」  安全性原則。 如需指派使用者權限的詳細資訊，請參閱 Windows 文件集。  
  
 當 TDE 啟用時，無法使用立即檔案初始化。  
  
 授與帳戶「 `Perform volume maintenance tasks` 」權限：  
  
1.  在將建立備份檔案的電腦上，開啟「`Local Security Policy`」應用程式 (`secpol.msc`)。  
  
2.  在左窗格中，展開 [本機原則] ，然後按一下 [使用者權限指派] 。  
  
3.  在右窗格中，按兩下 [執行磁碟區維護工作]。  
  
4.  按一下 [新增使用者或群組]  ，新增用於備份的任何使用者帳戶。  
  
5.  按一下 **套用**，然後關閉所有`Local Security Policy`對話方塊。  
  
### <a name="security-considerations"></a>安全性考量  
 刪除的磁碟內容只有在新資料寫入檔案時才會被覆寫，因此，未經授權的主體可能會存取刪除的內容。 當資料庫檔案附加到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的執行個體後，檔案上的任意存取控制清單 (DACL) 可降低此一資訊洩漏威脅。 此 DACL 只允許 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶和本機系統管理員存取檔案。 但是當檔案卸離後，沒有 SE_MANAGE_VOLUME_NAME 的使用者或服務便能存取該檔案。 備份資料庫時也存在類似的威脅。 如果備份檔案未使用適當的 DACL 保護，未經授權的使用者或服務便可存取刪除的內容。  
  
 如果洩漏刪除的內容可能是一項隱憂，您應該採取下列其中一項或兩項方法：  
  
-   務必確保所有卸離的資料檔和備份檔都具有限制的 DACL。  
  
-   停用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的立即檔案初始化，方法是從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶撤銷 SE_MANAGE_VOLUME_NAME。  
  
> [!NOTE]  
>  停用立即檔案初始化只會影響使用者權限撤銷後建立或大小增加的檔案。  
  
## <a name="see-also"></a>另請參閱  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)  
  
  

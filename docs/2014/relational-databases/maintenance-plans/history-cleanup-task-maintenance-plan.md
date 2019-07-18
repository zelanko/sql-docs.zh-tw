---
title: 記錄清除工作 (維護計畫) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql12.swb.maint.historycleanup.f1
helpviewer_keywords:
- History Cleanup Task dialog box
ms.assetid: 66bb6c39-958c-4053-a27f-b1118d2567f5
ms.reviewer: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a2b398a9910926ca2ced339395feaf938c31d519
ms.sourcegitcommit: 0a4879dad09c6c42ad1ff717e4512cfea46820e9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/27/2019
ms.locfileid: "67412700"
---
# <a name="history-cleanup-task-maintenance-plan"></a>記錄清除工作 (維護計畫)

  使用 **[記錄清除工作]** 對話方塊，即可從 msdb 資料庫的資料表中捨棄舊的記錄資訊。 這個工作支援備份和還原記錄、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業記錄，以及維護計畫記錄的刪除。  
  
 此陳述式會使用 **sp_purge_jobhistory** 和 **sp_delete_backuphistory** 陳述式。  
  
## <a name="uielement-list"></a>UIElement 清單  
 **[連接]**  
 選取執行此工作時要使用的伺服器連接。  
  
 **新增**  
 建立新的伺服器連接，以便執行此工作時使用。 **[新增連接]** 對話方塊會在本主題稍後描述。  
  
 **備份與還原記錄**  
 保留最近建立備份時的記錄，有助於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在您要還原資料庫時，建立復原計畫。 保留期限至少應該是完整資料庫備份的頻率。  
  
 **SQL Server Agent 作業記錄**  
 這個記錄可以幫助您疑難排解失敗的作業，或判斷資料庫動作為何發生。  
  
 **維護計畫記錄**  
 這個記錄可以幫助您疑難排解失敗的維護計畫作業，或判斷資料庫動作為何發生。  
  
 **移除早於下列時限的記錄資料**  
 指定您想要刪除的項目之存在時間。  
  
 **檢視 T-SQL**  
 根據選取的選項，檢視此工作在伺服器上執行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。  
  
> [!NOTE]  
>  受影響的物件數目較為大量時，會多花一些時間才會顯示。  
  
## <a name="new-connection-dialog-box"></a>新增連接對話方塊  
 **連接名稱**  
 輸入新連接的名稱。  
  
 **選取或輸入伺服器名稱**  
 選取執行此工作時要連接的伺服器。  
  
 **[重新整理]**  
 重新整理可用的伺服器清單。  
  
 **輸入要登入到伺服器的資訊**  
 指定如何對伺服器進行驗證。  
  
 **使用 Windows 整合式安全性**  
 使用 Microsoft Windows 驗證來連接 SQL Server [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體。  
  
 **使用特定的使用者名稱和密碼**  
 使用 SQL Server 驗證來連接 SQL Server [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體。 無法使用此選項。  
  
 **使用者名稱**  
 提供驗證時要使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。 無法使用此選項。  
  
 **密碼**  
 提供驗證時要使用的密碼。 無法使用此選項。  
  
## <a name="see-also"></a>另請參閱  
 [sp_purge_jobhistory &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-purge-jobhistory-transact-sql)   
 [sp_delete_backuphistory &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql)  
  
  

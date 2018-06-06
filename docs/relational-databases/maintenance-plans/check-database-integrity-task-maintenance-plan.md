---
title: 檢查資料庫完整性工作 (維護計畫) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: maintenance-plans
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.maint.maintplanproperties.integrity.f1
- sql13.swb.maint.integrity.f1
helpviewer_keywords:
- Check Database Integrity Task dialog box
ms.assetid: 3534494a-5dfe-4738-b49a-e7fabd731c47
caps.latest.revision: 24
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: bed0e36e8e6ac82e642942ea208e9378de365136
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="check-database-integrity-task-maintenance-plan"></a>檢查資料庫完整性工作 (維護計畫)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  使用 [檢查資料庫完整性工作] 對話方塊，並執行 `DBCC CHECKDB`[!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式，以檢查使用者和系統資料表的配置和結構完整性以及資料庫的索引。 執行 `DBCC` 以確實回報任何有關資料庫完整性的問題，以便系統管理員或資料庫擁有者稍後解決。  
  
## <a name="options"></a>選項。  
 **[連接]**  
 選取執行此工作時要使用的伺服器連接。  
  
 **新增**  
 建立新的伺服器連接，以便執行此工作時使用。 下面會描述 **[新增連接]** 對話方塊。  
  
 **資料庫**  
 指定受此工作影響的資料庫。  
  
-   **所有資料庫**  
  
     產生維護計畫，針對所有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫執行維護工作，但 **tempdb**除外。  
  
-   **所有系統資料庫**  
  
     產生維護計畫，針對每個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統資料庫執行維護工作，但 **tempdb**除外。 不會針對使用者建立的資料庫執行維護工作。  
  
-   **所有使用者資料庫**  
  
     產生維護計畫，針對所有使用者建立的資料庫執行維護工作。 不會對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統資料庫執行任何維護工作。  
  
-   **這些特定的資料庫**  
  
     產生維護計畫，只針對選取的資料庫執行維護工作。 如果選擇此選項，則必須在清單中至少選取一個資料庫。  
  
    > [!NOTE]  
    >  維護計畫只針對相容性層級設為 80 (含) 以上的資料庫來執行。 不會顯示相容性層級設為 70 或更低的資料庫。  
  
 **包含索引**  
 檢查所有的索引頁面以及資料表資料頁面的完整性。  
  
 **僅限實體**  
 將檢查限制於頁面實體結構、記錄標頭的完整性，以及資料庫配置的一致性。 使用此選項可縮短 DBCC CHECKDB 對大型資料庫的執行階段，因此，建議您在實際系統上經常使用。  
  
 **Tablock**  
 使 DBCC CHECKDB 取得鎖定，而不使用內部資料庫快照集。 這包括資料庫上的短期獨佔 (X) 鎖定。 使用此選項可協助 DBCC CHECKDB 在負載沉重的資料庫上執行得快一些，但 DBCC CHECKDB 執行時，資料庫可用的並行會降低。  
  
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
 使用 Windows 驗證連接 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體。  
  
 **使用特定的使用者名稱和密碼**  
 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。 無法使用此選項。  
  
 **User name**  
 提供驗證時要使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。 無法使用此選項。  
  
 **密碼**  
 提供驗證時要使用的密碼。 無法使用此選項。  
  
## <a name="see-also"></a>另請參閱  
 [DBCC CHECKDB &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)  
  
  

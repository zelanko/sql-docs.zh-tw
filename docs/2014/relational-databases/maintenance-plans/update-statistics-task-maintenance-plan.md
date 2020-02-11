---
title: 更新統計資料工作 (維護計畫) | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql12.swb.maint.statistics.f1
helpviewer_keywords:
- Updates Statistics Task dialog box
ms.assetid: 22902fd0-eb39-4f18-af94-3fcb69d2a3a4
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 51a3deffc9db182f7b3ad8f50d27c24e0f74dc6d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62807070"
---
# <a name="update-statistics-task-maintenance-plan"></a>更新統計資料工作 (維護計畫)
  使用 [**更新統計資料**工作] 對話方塊[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，即可更新資料表和索引中資料的相關資訊。 此工作針對資料庫中使用者資料表所建立的每個索引，重新取樣散發統計資料。 在處理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 陳述式的期間， [!INCLUDE[tsql](../../includes/tsql-md.md)] 會使用散發統計資料來最佳化資料表的導覽。 若要自動建立散發統計資料， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會在每個索引的對應資料表中，定期地取樣資料。 取樣大小會視資料表的資料列數與資料修改的頻率而定。 使用此選項即可使用資料表中指定的資料百分比執行其他取樣。 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會使用此資訊來建立更好的查詢計畫。  
  
 此工作會執行 UPDATE STATISTICS 陳述式。  
  
## <a name="options"></a>選項。  
 **[連接]**  
 選取執行此工作時要使用的伺服器連接。  
  
 **新增**  
 建立新的伺服器連接，以便執行此工作時使用。 下面會描述 **[新增連接]** 對話方塊。  
  
 **資料庫**  
 指定受此工作影響的資料庫。  
  
-   **所有資料庫**  
  
     產生維護計畫，針對所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫執行維護工作，但 tempdb 除外。  
  
-   **所有系統資料庫**  
  
     產生維護計畫，針對每個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統資料庫執行維護工作，但 tempdb 除外。 不會針對使用者建立的資料庫執行維護工作。  
  
-   **所有使用者資料庫**  
  
     產生維護計畫，針對所有使用者建立的資料庫執行維護工作。 不會對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統資料庫執行任何維護工作。  
  
-   **這些特定的資料庫**  
  
     產生維護計畫，只針對選取的資料庫執行維護工作。 如果選擇此選項，則必須在清單中至少選取一個資料庫。  
  
 **注意**維護計畫只會針對設定為相容性層級80或更高版本的資料庫執行。 不會顯示相容性層級設為 70 或更低的資料庫。  
  
 **Object**  
 限制 [選取範圍]**** 格線僅顯示資料表、檢視或兩者。  
  
 **選取項目**  
 指定受此工作影響的資料表或索引。 [物件] 方塊中的 **[資料表和檢視]** 為選取狀態時無法使用。  
  
 **所有現有的統計資料**  
 同時更新資料行與索引的統計資料。  
  
 **僅限資料行統計資料**  
 僅更新資料行統計資料。  
  
 **僅限索引統計資料**  
 僅更新索引統計資料。  
  
 **掃描類型**  
 用來蒐集更新統計資料的掃描類型。  
  
 **完整掃描**  
 讀取資料表或檢視中的所有資料列來蒐集統計資料。  
  
 **範例依據**  
 當收集較大資料表或檢視的統計資料時，指定要取樣的資料表或索引檢視百分比或資料列數。  
  
 **View T-sql**  
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
  
 **輸入資訊以登入伺服器**  
 指定如何對伺服器進行驗證。  
  
 **使用 Windows 整合式安全性**  
 使用[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 驗證連接到的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]實例。  
  
 **使用特定的使用者名稱和密碼**  
 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 驗證，連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。 無法使用此選項。  
  
 **使用者名稱**  
 提供驗證時要使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。 無法使用此選項。  
  
 **密碼**  
 提供驗證時要使用的密碼。 無法使用此選項。  
  
## <a name="see-also"></a>另請參閱  
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/update-statistics-transact-sql)  
  
  

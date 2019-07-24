---
title: 修復失敗的 SQL Server 安裝 | Microsoft Docs
ms.custom: ''
ms.date: 09/08/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 90c11b28-892b-44d6-978e-0eee48c75b7d
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 9130fd4fae0660008ede059418179b1bb9777a9e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67990844"
---
# <a name="repair-a-failed-sql-server-installation"></a>修復失敗的 SQL Server 安裝

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

下列情況下可以使用修復作業：  
  
- 修復成功安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體之後卻又損毀的執行個體。 
  
- 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體名稱對應到新升級的執行個體之後，升級作業遭到取消或失敗，請修復這個執行個體。 
  
    - 如果您在摘要記錄檔中看到以下訊息，您可以修復失敗的升級執行個體：  
  
         「[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 升級失敗。 若要繼續，請調查失敗的原因、更正問題，然後修復安裝。」  
  
    - 如果您在摘要記錄檔中看到以下訊息，您需要解除安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]然後再重新安裝。 您無法修復 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。 
  
         「[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 升級失敗。 若要繼續，請調查失敗的原因並更正問題。」  
  
 當您修復 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的執行個體時：  
  
- 所有遺失或損毀的檔案都會被取代 
  
- 所有遺失或損毀的登錄機碼都會被取代 
  
- 所有遺失或無效的組態值都會設為預設值。 
  
 繼續進行之前，請針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集，檢閱下列重要資訊：  
  
- 您必須在個別的叢集節點上執行修復。 
  
- 若要在失敗的「準備」作業之後修復容錯移轉叢集節點，請使用 [移除節點]  ，然後再次執行「準備」步驟。 如需詳細資訊，請參閱[在 SQL Server 容錯移轉叢集中新增或移除節點 &#40;安裝程式&#41;](../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)。 
  
## <a name="repair-a-failed-installation-of-includessnoversionincludesssnoversion-mdmd-from-the-installation-center"></a>從安裝中心修復失敗的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝 
  
1. 從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝媒體啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式 (setup.exe)。 
  
2. 驗證必要元件和系統之後，安裝程式將會顯示 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝中心] 頁面。 
  
3. 按一下左側導覽區域中的 [維護]  ，然後按一下 [修復]  啟動修復作業。 
  
   >[!TIP]  
   > 如果使用 [開始] 功能表啟動安裝中心，您將需要在這個階段提供安裝媒體的位置。 
  
4. 安裝程式支援規則和檔案常式將會執行，以便確保您的系統已安裝必要元件而且電腦通過安裝程式驗證規則。 按一下 **[確定]** 或 **[安裝]** 繼續進行。 
  
5. 在 [選取執行個體] 頁面上，選取要修復的執行個體，然後按一下 [下一步]  繼續進行。 
  
6. 修復規則將會執行，以便驗證作業。 若要繼續進行，請按 **[下一步]** 。 
  
7. [已完成修復準備工作] 頁面會指出作業準備繼續進行。 若要繼續，請按一下 [修復]  。 
  
8. [修復進度] 頁面會顯示修復作業的狀態。 [完成] 頁面會指出作業已完成。 
  
### <a name="to-repair-a-failed-installation-of-includessnoversionincludesssnoversion-mdmd-using-command-prompt"></a>若要使用命令提示字元修復失敗的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝  
  
1. 在命令提示字元執行下列命令：  
  
    ```  
    Setup.exe /q /ACTION=Repair /INSTANCENAME=instancename  
    ```  
  
## <a name="see-also"></a>另請參閱  
 [檢視與讀取 SQL Server 安裝程式記錄檔](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)   
 [安裝的使用說明文章](https://msdn.microsoft.com/library/59de41e7-557f-462a-8914-53ec35496baa)  
  
  

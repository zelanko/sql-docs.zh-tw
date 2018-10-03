---
title: SQL Server 屬性 （AlwaysOn 高可用性 索引標籤） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- configmgr-client
ms.topic: conceptual
ms.assetid: d8630923-a600-4f1c-aca1-027453a3ec82
author: mikeraymsft
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 91aedc290389f317a04263a1bbdde2bb086226a5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48062658"
---
# <a name="sql-server-properties-alwayson-high-availability-tab"></a>SQL Server 屬性 (AlwaysOn 高可用性索引標籤)
  使用**AlwaysOn 高可用性**索引標籤**SQL Server 屬性** 對話方塊中的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]組態管理員來啟用或停用 AlwaysOn 可用性群組功能，在[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. 啟用 AlwaysOn 可用性群組是的執行個體的必要條件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用可用性群組做為高可用性和災害復原方案。  
  
##  <a name="Prerequisites"></a> 必要條件  
 若要啟用 AlwaysOn 可用性群組，伺服器執行個體必須符合下列必要條件：  
  
-   此伺服器執行個體必須位於 Windows Server 容錯移轉叢集 (WSFC) 節點上。  
  
-   若要位於相同的可用性群組，執行個體必須位於相同的 WSFC 叢集中。 可用性群組不可跨越多個 WSFC 叢集。  
  
-   伺服器執行個體必須執行支援 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]版本。  
  
-   一次只針對一個伺服器執行個體啟用 AlwaysOn 可用性群組。 啟用 AlwaysOn 可用性群組之後，等到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之前啟用的下一步 的伺服器執行個體重新啟動服務。  
  
> [!NOTE]  
>  如需功能支援的詳細資訊，以及有關 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]其他必要條件、限制和建議的詳細資訊，請參閱《 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 線上叢書》。  
  
## <a name="dialog-options"></a>對話方塊選項  
 **Windows 容錯移轉叢集名稱**  
 顯示本機電腦為其節點之 WSFC 叢集的名稱。  
  
 **啟用 AlwaysOn 可用性群組**  
 使用此核取方塊，在這個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上啟用或停用 AlwaysOn 可用性群組，如下所示：  
  
-   如果此核取方塊是空的，表示 AlwaysOn 可用性群組目前停用。 若要啟用 AlwaysOn 可用性群組，請選取此核取方塊，按一下 **[確定]**，然後手動重新啟動[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服務。  
  
-   如果已選取此核取方塊，表示 AlwaysOn 可用性群組目前啟用。 若要停用 AlwaysOn 可用性群組，請取消核取此核取方塊，按一下**確定**。 這樣伺服器執行個體就會重新啟動。  
  
    > [!TIP]  
    >  停用 AlwaysOn 可用性群組之後，您應該從伺服器執行個體中移除任何本機可用性複本。 如果移除指定可用性群組的最後一個複本，同時也應該移除此群組。  
  
## <a name="uielement-list"></a>UIElement 清單  
  
> [!NOTE]  
>  如需有關停用 AlwaysOn 可用性群組之後的後續動作資訊，以及有關如何建立及設定可用性群組的詳細資訊，請參閱《[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 線上叢書》。  
  
  

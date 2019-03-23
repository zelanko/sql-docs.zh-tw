---
title: 叢集中的 Integration Services (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 0216266d-d866-4ea2-bbeb-955965f4d7c2
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b70dbab14424335fe210f5a9b1ddbdbda4f90deb
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2019
ms.locfileid: "58392860"
---
# <a name="integration-services-ssis-in-a-cluster"></a>叢集中的 Integration Services (SSIS)
  不建議您以叢集方式設定 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]，因為 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務不是叢集服務或叢集感知的服務，也不支援從一個叢集節點容錯移轉到另一個叢集節點。 因此，在叢集環境中，應該以獨立服務的形式在叢集中的每一個節點上安裝及啟動 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 。  
  
 雖然 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務並非叢集服務，但在叢集的每個節點上個別安裝 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 之後，您可以手動設定該服務，把它當做叢集資源來運作。  
  
 不過，如果您在建立叢集硬體環境時的目標是高可用性，則就算不將 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務設定為叢集資源，也可以達到此目標。  若要從叢集的任何其他節點來管理叢集中任何節點上的封裝，請在叢集中的每個節點上修改 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務的組態檔。 您要將每個組態檔修改成指向封裝儲存所在的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的所有可用執行個體。 這個方案能提供大多數客戶所需的高可用性，而沒有將 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務設定為叢集資源時可能遇到的問題。 如需如何變更組態檔的詳細資訊，請參閱[設定 Integration Services 服務 &#40;SSIS 服務&#41;](integration-services-service-ssis-service.md)。  
  
 若要針對如何在叢集環境中設定服務而進行資訊完整的決策，了解 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務的角色是很重要的。 如需詳細資訊，請參閱 [Integration Services Service &#40;SSIS Service&#41;](integration-services-service-ssis-service.md) (Integration Services 服務 (SSIS 服務))。  
  
## <a name="understanding-the-disadvantages-of-configuring-integration-services-as-a-cluster-resource"></a>了解將 Integration Services 設定為叢集資源的缺點  
 將 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務設定為叢集資源的一些可能缺點包括下列：  
  
-   當容錯移轉發生時，執行中的封裝不會重新啟動。 您可以藉由從檢查點重新啟動封裝而從封裝失敗復原。 如果不將服務設定為叢集資源，就可以從檢查點重新啟動。 如需詳細資訊，請參閱 [使用檢查點來重新啟動封裝](../packages/restart-packages-by-using-checkpoints.md)。  
  
-   當您在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的不同資源群組中設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服務時，無法從用戶端電腦使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 來管理儲存在 msdb 資料庫中的封裝。 在這種雙躍點的狀況中， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務無法委派認證。  
  
-   如果您擁有多個在叢集中包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 資源群組，則容錯移轉可能會導致非預期的結果。 請考慮下列狀況。 包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務和 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務的「群組 1」在「節點 A」上執行。另一也包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務和 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務的「群組 2」則在「節點 B」上執行。「群組 2」容錯移轉至「節點 A」。在「節點 A」上啟動 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務另一個執行個體的嘗試失敗，因為 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務是單一執行個體的服務。 正嘗試容錯移轉至「節點 A」的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務是否也會失敗，是根據「群組 2」中的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務的設定而定。 如果將 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務設定為影響資源群組中的其他服務，則正在進行容錯移轉的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務將會失敗，因為 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務已失敗。 如果服務是設定為不影響資源群組中的其他服務，則 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務就可以容錯移轉至「節點 A」。除非「群組 2」中的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務是設定為不影響資源群組中的其他服務，否則如果正在容錯移轉的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務失敗，可能會導致正在容錯移轉的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務也失敗。  
  
## <a name="related-tasks"></a>相關工作  
 如需在叢集中設定 Integration Services 服務的逐步指示，請參閱 [將 Integration Services 服務設定為叢集資源](../configure-the-integration-services-service-as-a-cluster-resource.md)。  
  
  

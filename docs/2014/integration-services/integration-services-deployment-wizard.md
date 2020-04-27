---
title: Integration Services 部署嚮導 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.deploymentwizard.f1
ms.assetid: f3d93e13-2d85-47ff-a913-cda4046491c4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 721953c31a44a2ea02f480c9830e6347adfd4eb3
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66058012"
---
# <a name="integration-services-deployment-wizard"></a>Integration Services 部署精靈
  「[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 部署精靈」會使用專案部署模型，將專案部署至 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體上的 SSISDB 目錄。  
  
 若要從[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]中[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]開啟的專案啟動部署嚮導，請從 [**專案**] 功能表中選取 [**部署**]。 若[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]要在中啟動精靈，請在物件總管中展開 [ **Integration Services 目錄** > **SSISDB** ] 節點，以滑鼠右鍵按一下 [**專案**] 資料夾，然後按一下 [**部署專案**]。  
  
 此精靈會繼續進行下列四個步驟。 按 **[下一步]** 移至下一個步驟，或按一下 [**上**一步] 返回上一個步驟。  
  
1.  **選取來源**-選取您[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]要部署的專案。  
  
2.  **選取目的地**-選取專案目的地。  
  
3.  **審查**-顯示您的選擇。  
  
4.  **部署/結果**-部署專案並顯示結果。  
  
## <a name="select-source"></a>選取來源  
 若要部署您建立的專案部署檔案，請選取 [**專案部署**檔案]，並輸入 .ispac 檔案的路徑，或按一下 **[流覽]** ， [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]在專案資料夾中尋找檔案。 若要部署位於 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 目錄中的專案，請選取 **[Integration Services 目錄]**，然後輸入伺服器名稱以及該專案在目錄中的路徑。  
  
 如果您在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 中啟動精靈，則該精靈預設會選取已開啟的專案做為來源，並略過此步驟。 若要返回此步驟並選取不同的來源，請按一下 [**上一**步]，或按一下左窗格中的 [**選取來源**]。  
  
## <a name="select-destination"></a>選取目的地  
 若要選取專案在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 目錄中的目的地資料夾，請輸入 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體，或按一下 **[瀏覽]** ，從伺服器清單中選取。 在 SSISDB 中輸入專案路徑，或按一下 **[瀏覽]** 來選取路徑。  
  
 如果您在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中啟動精靈，則該精靈預設會選取已連接的伺服器執行個體，並輸入所選專案的路徑。 您可以變更這些值，以便將專案部署至不同的位置。  
  
## <a name="review"></a>檢閱  
 此精靈可讓您在部署專案之前，先檢閱您所選取的設定。 您可以按一下 **[上一步]**，或按一下左窗格中的任何步驟來變更您的選取項目。  
  
## <a name="deployresults"></a>部署/結果  
 當您從 [**審核**] 頁面按一下 [**部署**] 時，會部署專案，而 [**結果**] 頁面會顯示每個動作的成功或失敗。 如果動作失敗，按一下 **[結果]** 資料行中的 **[失敗]** 以顯示錯誤的說明。 按一下 [**儲存報表**]，將結果儲存至 XML 檔案。  
  
 按一下 [關閉]**** 以結束精靈。  
  
## <a name="see-also"></a>另請參閱  
 [將專案部署至 Integration Services 伺服器](../../2014/integration-services/deploy-projects-to-integration-services-server.md)   
 [部署專案和封裝](packages/deploy-integration-services-ssis-projects-and-packages.md)  
  
  

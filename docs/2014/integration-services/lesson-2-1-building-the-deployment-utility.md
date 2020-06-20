---
title: 步驟 1：建置部署公用程式 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 1ff4dcff-89b3-4b99-a725-5f7963e98abf
author: janinezhang
ms.author: janinez
ms.openlocfilehash: c8c0cc7df39c8b5bac3ff216aa3d61975c707207
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84966088"
---
# <a name="step-1-building-the-deployment-utility"></a>步驟 1:建置部署公用程式
  在這項工作中，您將設定並建立「部署教學課程」專案的部署公用程式。  
  
 您必須先修改「部署教學課程」專案的屬性，才能建立部署公用程式。 您將使用 [Deployment Tutorial Property Pages (部署教學課程屬性頁)]  對話方塊來設定這些屬性。 在這個對話方塊中，您必須啟用能夠在部署期間更新組態的能力，而且指定建立期間產生部署公用程式。 在設定完屬性後，您將建立專案。  
  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 提供一組可用來偵錯套件的視窗。 您可以檢視錯誤、警告和資訊訊息、在執行階段追蹤有關封裝的狀態，或是檢視建立過程的進度及結果。 在本課程中，您將使用 [輸出] 視窗來檢視建立部署公用程式的進度及結果。  
  
### <a name="to-set-the-deployment-utility-properties"></a>設定部署公用程式屬性  
  
1.  如果尚未開啟 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]，請按一下 [開始]  ，依序指向 [所有程式]  和 [Microsoft SQL Server]  ，然後按一下 [Business Intelligence Development Studio]  。  
  
2.  在 [檔案]  功能表上，依序按一下 [開啟]  、[專案/方案]  和 [部署教學課程]  資料夾，然後按一下 [開啟]  ，再按兩下 [Deployment Tutorial.sln]  。  
  
3.  在方案總管中，以滑鼠右鍵按一下 [Deployment Tutorial (部署教學課程)]，然後按一下 [屬性]  。  
  
4.  在 [Deployment Tutorial Property Pages (部署教學課程屬性頁)]  對話方塊中，展開 [組態屬性]，然後按一下 [部署公用程式]。  
  
5.  在 [**部署教學課程屬性頁**] 對話方塊的右窗格中，確認 `AllowConfigurationChanges` 已設定為 `true` 、將設 `CreateDeploymentUtility` 為 `true` ，並選擇性地更新的預設值 `DeploymentOutputPath` 。  
  
6.  按一下 [確定]  。  
  
### <a name="to-build-the-deployment-utility"></a>建立部署公用程式  
  
1.  在方案總管中，按一下 [Deployment Tutorial (部署教學課程)]  。  
  
2.  在 [檢視]  功能表上，按一下 [輸出]  。 根據預設值，[輸出] 視窗是位在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]的左下角。  
  
3.  在 [建立]  功能表上，按一下 [Build Deployment Tutorial (建立部署教學課程)]  。  
  
4.  在 [輸出] 視窗中，確認以下資訊：  
  
     已經開始建立: SQL Integration Services 專案: 累加 ...  
  
     正在建立部署公用程式...  
  
     已建立部署公用程式。  
  
     建立已完成 -- 0 個錯誤，0 個警告  
  
     ========== 建置: 0 成功、0 失敗、1 最新、0 略過 ==========  
  
5.  在 **[檔案]** 功能表上按一下 **[結束]** 。 如果出現對 [Deployment Tutorial (部署教學課程)] 項目儲存變更的提示，請按一下 [是]  。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [步驟 2：確認部署配套](../integration-services/lesson-2-2-verifying-the-deployment-bundle.md)  
  
![Integration Services 圖示（小型）](media/dts-16.gif "Integration Services 圖示 (小)")**與 Integration Services 保持最**新狀態  <br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。  
  
## <a name="see-also"></a>另請參閱  
 [Create a Deployment Utility](../../2014/integration-services/create-a-deployment-utility.md)  
  
  

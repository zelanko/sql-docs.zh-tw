---
title: 步驟 1：建置部署公用程式 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 1ff4dcff-89b3-4b99-a725-5f7963e98abf
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 47d98801dd722f1727a7cdf3a982bf63cbd9974e
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86917294"
---
# <a name="lesson-2-1---building-the-deployment-utility"></a>第 2-1 課：建置部署公用程式

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


在這項工作中，您將設定並建立「部署教學課程」專案的部署公用程式。  
  
您必須先修改「部署教學課程」專案的屬性，才能建立部署公用程式。 您將使用 [Deployment Tutorial Property Pages (部署教學課程屬性頁)]  對話方塊來設定這些屬性。 在這個對話方塊中，您必須啟用能夠在部署期間更新組態的能力，而且指定建立期間產生部署公用程式。 在設定完屬性後，您將建立專案。  
  
[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 提供一組可用來偵錯套件的視窗。 您可以檢視錯誤、警告和資訊訊息、在執行階段追蹤有關封裝的狀態，或是檢視建立過程的進度及結果。 在本課程中，您將使用 [輸出] 視窗來檢視建立部署公用程式的進度及結果。  
  
### <a name="to-set-the-deployment-utility-properties"></a>設定部署公用程式屬性  
  
1.  如果尚未開啟 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]，請按一下 [開始]  ，依序指向 [所有程式]  和 [Microsoft SQL Server]  ，然後按一下 [Business Intelligence Development Studio]  。  
  
2.  在 [檔案]  功能表上，依序按一下 [開啟]  、[專案/方案]  和 [部署教學課程]  資料夾，然後按一下 [開啟]  ，再按兩下 [Deployment Tutorial.sln]  。  
  
3.  在方案總管中，以滑鼠右鍵按一下 [Deployment Tutorial (部署教學課程)]，然後按一下 [屬性]  。  
  
4.  在 [Deployment Tutorial Property Pages (部署教學課程屬性頁)]  對話方塊中，展開 [組態屬性]，然後按一下 [部署公用程式]。  
  
5.  在 [Deployment Tutorial Property Pages (部署教學課程屬性頁)]  對話方塊的右邊窗格中，確認 **AllowConfigurationChanges** 是設為 **true**，再將 **CreateDeploymentUtility** 設為 **true**，並選擇性更新 **DeploymentOutputPath** 的預設值。  
  
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
  
## <a name="see-also"></a>另請參閱  
[建立部署公用程式](../integration-services/packages/create-a-deployment-utility.md)  
  
  
  

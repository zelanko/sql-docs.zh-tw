---
title: 指定安裝目標 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- input files [Analysis Services]
- installation targets [Analysis Services]
- Analysis Services deployments, installation targets
- Analysis Services Deployment Wizard, installation targets
- deploying [Analysis Services], installation targets
- modifying installation targets
ms.assetid: cb706817-6f63-4771-92c3-b70030bbce3d
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 3e2f46eeb01baa5f6f208a612ecba5ad61dad004
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36135276"
---
# <a name="specifying-the-installation-target"></a>指定安裝目標
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]部署精靈會讀取安裝目標資訊從\<*專案名稱*> placeholder>>.deploymenttargets 檔案。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 會在您建立 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案時建立此檔案。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 會使用資料庫和伺服器上指定**部署**頁面*\<專案名稱 >* **屬性頁**對話方塊來建立\<*專案名稱*>.targets 檔案。  
  
## <a name="modifying-the-installation-target-for-deployment"></a>修改部署的安裝目標  
 在某些情況下，您可能需要將 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案部署到與 [部署] 頁面所指定之不同的資料庫或 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體上。 例如，您可能需要在部署之前先將專案部署到伺服器以進行測試，然後在測試完成後再部署到實際伺服器。 您也可能需要將完整與測試的專案部署到網路負載平衡叢集中的多個實際伺服器，或部署到臨時伺服器和實際伺服器。  
  
 若要將 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案部署到不同的資料庫或 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體，您可以使用下列程序描述的方法之一，來變更輸入檔中的安裝目標。  
  
#### <a name="to-change-the-installation-target-after-the-input-files-have-been-generated"></a>若要在已產生輸入檔之後，變更安裝目標  
  
-   以互動方式執行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈。 在 [安裝目標] 頁面上，指定 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體和資料庫的新目的地。  
  
     – 或 –  
  
-   在命令提示字元下執行 [ [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈]，並將精靈設定為以回應檔案模式執行。 如需回應檔案模式的詳細資訊，請參閱 [執行 Analysis Services 部署精靈](running-the-analysis-services-deployment-wizard.md)。  
  
     – 或 –  
  
-   修改\<*專案名稱*> placeholder>>.deploymenttargets 檔案使用任何文字編輯器。  
  
## <a name="see-also"></a>另請參閱  
 [指定資料分割和角色部署選項](deployment-script-files-partition-and-role-deployment-options.md)   
 [指定方案部署的組態設定](deployment-script-files-solution-deployment-config-settings.md)   
 [指定處理選項](deployment-script-files-specifying-processing-options.md)  
  
  
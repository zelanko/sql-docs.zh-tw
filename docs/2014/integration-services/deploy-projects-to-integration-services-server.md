---
title: 將專案部署到 Integration Services Server |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 6e9402f4-4d50-49ff-820d-65a77829c4a5
author: janinezhang
ms.author: janinez
ms.openlocfilehash: a41158c6ab83491c10c702619a9da46f096a4bfa
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84951680"
---
# <a name="deploy-projects-to-integration-services-server"></a>將專案部署至 Integration Services 伺服器
  在目前版本的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]中，您可以將專案部署到 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 伺服器。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 伺服器可讓您管理封裝、執行封裝，以及利用環境設定封裝的執行值。  
  
 如需環境的詳細資訊，請參閱 [建立和對應伺服器環境](../../2014/integration-services/create-and-map-a-server-environment.md)。  
  
> [!NOTE]  
>  與舊版 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]相同，在目前版本中，您也可以將封裝部署至 SQL Server 的執行個體，以及使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務來執行和管理封裝。 您會使用封裝部署模型。 如需詳細資訊，請參閱[&#40;SSIS&#41;的封裝部署](packages/legacy-package-deployment-ssis.md)。  
  
 如果要將專案部署至 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 伺服器，請完成下列工作：  
  
1.  建立 SSISDB 目錄 (如果尚未建立)。 如需詳細資訊，請參閱 [建立 SSIS 目錄](catalog/ssis-catalog.md)。  
  
2.  請執行 [Integration Services 專案轉換精靈]**** 將專案轉換為專案部署模型。 如需詳細資訊，請參閱底下指示： [將專案轉換為專案部署模型](#convert)  
  
    -   若您將專案建立在 [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)]中，則專案會根據預設使用專案部署模型。  
  
    -   若是在舊版 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]中建立專案，在您於 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]中開啟專案檔案後，請將專案轉換為專案部署模型。  
  
        > [!NOTE]  
        >  如果專案包含一個或多個資料來源，則在完成專案轉換時，會移除資料來源。 若要建立專案中的封裝可以共用的資料來源連接，請在專案層級加入連接管理員。 如需詳細資訊，請參閱 [加入、刪除或共用封裝中的連線管理員](../../2014/integration-services/add-delete-or-share-a-connection-manager-in-a-package.md)。  
  
         根據您是從 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 還是從 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 執行 [Integration Services 專案轉換精靈]****，此精靈會執行不同的轉換工作。  
  
        -   如果您是從 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]執行此精靈，則專案中包含的封裝會從 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 2005、2008 或 2008 R2 轉換為目前版本的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]使用的格式。 系統將會升級原始專案 (.dtproj) 和封裝 (.dtsx) 檔。  
  
        -   如果您是從 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]執行此精靈，此精靈將會從專案中包含的封裝和組態產生專案部署檔案 (.ispac)。 系統將不會升級原始封裝 (.dtsx) 檔。  
  
             您可以在精靈的 [選取目的地]**** 頁面中選取現有的檔案，或建立一個新檔案。  
  
             若要在轉換專案時升級封裝檔，請從 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 執行 [Integration Services 專案轉換精靈]****。 若要從專案轉換個別升級封裝檔案，請從 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 執行 [Integration Services 專案轉換精靈]****，然後執行 [SSIS 封裝升級精靈]****。 若您個別升級封裝檔，請確認是否儲存變更。 否則，當您將專案轉換成專案部署模型時，所有未儲存的封裝變更將不予轉換。  
  
     如需封裝升級的詳細資訊，請參閱 [升級 Integration Services 封裝](install-windows/upgrade-integration-services-packages.md) 和 [使用 SSIS 封裝升級精靈來升級 Integration Services 封裝](install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)。  
  
3.  將專案部署至 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 伺服器。 如需詳細資訊，請參閱底下指示： [將專案部署至 Integration Services 伺服器](#deploy)。  
  
4.  (選擇性) 建立部署專案的環境。 如需詳細資訊，請參閱 [建立和對應伺服器環境](../../2014/integration-services/create-and-map-a-server-environment.md)。  
  
##  <a name="to-convert-a-project-to-the-project-deployment-model"></a><a name="convert"></a>若要將專案轉換為專案部署模型  
  
1.  開啟 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 中的專案，然後在方案總管中，以滑鼠右鍵按一下該專案，並按一下 [轉換為專案部署模型]****。  
  
     -或-  
  
     從 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 的物件總管中，以滑鼠右鍵按一下 [專案]**** 節點，然後選取 [匯入封裝]****。  
  
2.  完成精靈。 如需相關資訊，請參閱 [Integration Services Project Conversion Wizard](../../2014/integration-services/integration-services-project-conversion-wizard.md)。  
  
##  <a name="to-deploy-a-project-to-the-integration-services-server"></a><a name="deploy"></a>若要將專案部署至 Integration Services 伺服器  
  
1.  開啟 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 中的專案，然後從 [專案]**** 功能表中選取 [部署]****，以啟動 [Integration Services 部署精靈]****。  
  
     -或-  
  
     在中 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] ，展開 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]  >  物件總管中的 [ **SSISDB** ] 節點，然後找出您要部署之專案的 [專案] 資料夾。 以滑鼠右鍵按一下 [專案]**** 資料夾，然後按一下 [部署專案]****。  
  
     -或-  
  
     在命令提示字元中，從 **%ProgramFiles%\Microsoft SQL Server\110\DTS\Binn** 執行 **isdeploymentwizard.exe**。 64 位元的電腦上的 **%ProgramFiles(x86)%\Microsoft SQL Server\100\DTS\Binn**也有提供 32 位元版本的工具。  
  
2.  在 [選取來源]**** 頁面上，按一下 [專案部署檔案]**** 以選取專案的部署檔案。  
  
     -或-  
  
     按一下 [Integration Services 目錄]****，選取已經部署至 SSISDB 目錄的專案。  
  
3.  完成精靈。 如需詳細資訊，請參閱 [Integration Services 部署精靈](../../2014/integration-services/integration-services-deployment-wizard.md)。  
  
  

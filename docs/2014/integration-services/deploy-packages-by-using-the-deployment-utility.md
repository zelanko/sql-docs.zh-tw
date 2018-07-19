---
title: 使用部署公用程式來部署套件 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- packages [Integration Services], installing
- installing packages
- dependencies [Integration Services]
- deploying packages [Integration Services], installing
ms.assetid: eaf4b56e-2023-4d17-971c-703031da758c
caps.latest.revision: 56
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 78fe699eade5daa76a8d6f2a77e63a2c5019b815
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37203928"
---
# <a name="deploy-packages-by-using-the-deployment-utility"></a>Deploy Packages by Using the Deployment Utility
  當已建立部署公用程式，以從建立部署公用程式之電腦以外電腦上的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案安裝封裝時，必須首先將部署資料夾複製到目的地電腦。  
  
 部署資料夾的路徑是在為其建立部署公用程式之 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案的 DeploymentOutputPath 屬性中指定的。 預設路徑為 bin\Deployment (相對於 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案)。 如需詳細資訊，請參閱 [建立部署公用程式](../../2014/integration-services/create-a-deployment-utility.md)。  
  
 請使用「封裝安裝精靈」來安裝封裝。 若要啟動此精靈，請在將部署資料夾複製到伺服器後按兩下部署公用程式檔案。 此檔案名為 \<專案名稱>.SSISDeploymentManifest；您可以在目的地電腦的部署資料夾中找到這個檔案。  
  
> [!NOTE]  
>  根據所部署的封裝版本，如果有不同版本的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 並存安裝，可能會發生錯誤。 因為 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]所有版本的 .SSISDeploymentManifest 副檔名都相同，所以可能會發生這項錯誤。 按兩下此檔案就會針對最近安裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]版本 (可能與部署公用程式檔案的版本不同) 呼叫安裝程式 (dtsinstall.exe)。 若要解決此問題，請從命令列執行正確的 dtsinstall.exe 版本，並且提供部署公用程式檔案的路徑。  
  
 [封裝安裝精靈] 會逐步引導您將封裝安裝到檔案系統或 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 您可以利用下列方式來設定安裝：  
  
-   選擇用來安裝封裝的位置類型和位置。  
  
-   選擇用來安裝封裝相依性的位置。  
  
-   在封裝安裝在目標伺服器之後驗證封裝。  
  
 封裝之以檔案作為基礎的相依性總是安裝到檔案系統。 如果您將封裝安裝到檔案系統，則會將相依性安裝到為封裝指定的資料夾。 如果您將封裝安裝到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，則可指定要儲存以檔案基礎之相依性的資料夾。  
  
 如果封裝包含您要修改以用於目的地電腦的組態，則可使用精靈更新屬性的值。  
  
 除了使用 [封裝安裝精靈] 安裝封裝之外，還可以使用 **dtutil** 命令提示字元公用程式來複製和移動封裝。 如需詳細資訊，請參閱 [dtutil Utility](dtutil-utility.md)。  
  
### <a name="to-deploy-packages-to-an-instance-of-sql-server"></a>將封裝部署至 SQL Server 的執行個體  
  
1.  開啟目標電腦上的部署資料夾。  
  
2.  按兩下資訊清單檔 \<專案名稱>.SSISDeploymentManifest，以啟動 [套件安裝精靈]。  
  
3.  在 [部署 SSIS 封裝] 頁面上，選取 [SQL Server 部署] 選項。  
  
4.  選擇性地選取 [安裝之後驗證封裝]，以在將封裝安裝到目標伺服器後對其進行驗證。  
  
5.  在 [指定目標 SQL Server] 頁面上，指定要安裝封裝的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的執行個體，並選取驗證模式。 如果選取「[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 驗證」，則您必須提供使用者名稱和密碼。  
  
6.  在 [選取安裝資料夾] 頁面上，為要安裝的封裝相依性指定檔案系統中的資料夾。  
  
7.  如果封裝包括組態，則可透過更新 [設定封裝] 頁面上 [值] 清單中的值來編輯組態。  
  
8.  如果選擇在安裝後驗證封裝，請檢視已部署封裝的驗證結果。  
  
## <a name="see-also"></a>另請參閱  
 [封裝部署&#40;SSIS&#41;](packages/legacy-package-deployment-ssis.md)  
  
  

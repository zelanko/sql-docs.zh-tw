---
title: 使用精靈部署模型部署套件 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- deployment packages [Master Data Services], deploying
- models [Master Data Services], deploying a package
ms.assetid: 4f65dc60-0ff8-46e6-9988-5bc5b9603ad0
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 3b74a2de7cd9479552fdf560a324a93541496eaa
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52792790"
---
# <a name="deploy-a-model-deployment-package-by-using-the-wizard"></a>使用精靈部署模型部署封裝
  若要部署只包含模型物件的套件，請使用 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 模型部署精靈。 如果您需要部署包含資料的套件，請參閱 [使用 MDSModelDeploy 部署模型部署封裝](../../2014/master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md)。  
  
> [!IMPORTANT]  
>  封裝只能部署到之前建立封裝所使用的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本。 這表示，在 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 中建立的封裝無法部署到 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]。  
  
## <a name="prerequisites"></a>先決條件  
 若要執行此程序：  
  
-   在目標 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 環境中，您必須擁有存取 [系統管理] 功能區域的權限。  
  
-   模型部署封裝必須存在。 如需詳細資訊，請參閱 [使用精靈建立模型部署封裝](../../2014/master-data-services/create-a-model-deployment-package-by-using-the-wizard.md)。  
  
-   您必須是您要部署模型之環境中的管理員。 如需詳細資訊，請參閱 [管理員 &#40;Master Data Services&#41;](administrators-master-data-services.md)，您就可以在群組中加入及移除使用者。  
  
### <a name="to-deploy-a-model-deployment-package-of-model-objects-only"></a>若僅要部署模型物件的模型部署封裝  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[系統管理]**。  
  
2.  在 [模型檢視] 頁面上，從功能表列指向 [系統]，然後按一下 [部署]。  
  
3.  按一下 [模型部署精靈] 上的 [部署]。  
  
4.  按一下 **[瀏覽]**。  
  
5.  尋找您的部署套件 (.pkg 檔案)，然後按一下 [開啟]。  
  
6.  按 [下一步] 。  
  
7.  載入套件之後，按一下 [下一步]。  
  
8.  如果模型已存在，您可以選取 [更新現有模型] 來更新模型。 若要建立新的模型，請選取 [建立新模型]，然後在按 [下一步] 之後，輸入新模型的名稱。  
  
9. 按一下 [完成] 結束精靈。  
  
 **注意：**  
  
-   如果封裝中的訂用帳戶檢視現有模型中的訂閱檢視同名，要將檢視建立為*modelname.subscriptionviewname*。 如果此名稱已在使用中，則不會建立訂閱檢視。  
  
-   部署程序有四個步驟：  
  
    1.  建立模型物件。  
  
    2.  建立訂閱檢視。  
  
    3.  建立商務規則。  
  
    4.  擴展主要資料。  
  
-   當建立新的模型或複製的模型時，如果此程序在任何步驟期間失敗，就會刪除該模型。  
  
     更新模型時，如果此程序在前三個步驟的任何一個期間失敗，就不會繼續進行，但是，並不會回復已經進行的變更。 如果此程序在步驟 4 失敗，則會更新可以更新的成員。  
  
## <a name="next-steps"></a>後續步驟  
 使用者定義的中繼資料、檔案屬性及使用者和群組的權限不包含在模型部署封裝中。 在部署模型之後，您必須手動更新這些項目。 如需詳細資訊，請參閱：  
  
-   [新增中繼資料&#40;Master Data Services&#41;](../../2014/master-data-services/add-metadata-master-data-services.md)  
  
-   [指派模型物件權限 &#40;Master Data Services&#41;](../../2014/master-data-services/assign-model-object-permissions-master-data-services.md)  
  
## <a name="see-also"></a>另請參閱  
 [部署模型 &#40;Master Data Services&#41;](../../2014/master-data-services/deploying-models-master-data-services.md)  
  
  

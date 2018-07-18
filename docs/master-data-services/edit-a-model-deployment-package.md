---
title: 編輯模型部署套件 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6b0fdb7d-83dd-4392-9011-4ae642c471f1
caps.latest.revision: 7
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: dd772bb9231e92e54d91d00985556fec4f595ae3
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/12/2018
ms.locfileid: "35330322"
---
# <a name="edit-a-model-deployment-package"></a>編輯模型部署封裝

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  此主題描述如何在 MDS 中部署模型的選定部分，而不是整個模型。 若要這樣做，請使用模型封裝編輯器編輯 MDS 模型封裝。  
  
 模型封裝編輯器精靈可讓您選取要併入 MDS 封裝中的特定實體、衍生階層、訂閱檢視和模型中的商務規則，並在之後加以部署。 您可以不處理模型中不想要部署的部分。 當您選取實體時，也會自動選取該實體中的所有相依物件。  
  
 您會使用模型封裝編輯器來選取封裝檔案中模型的部分，這個檔案是由 MDSModelDeploy 工具 (它所建立的封裝檔案包含物件和資料) 或模型部署精靈 (它所建立的檔案只包含模型結構) 所建立。 在編輯封裝中的模型之後，您會使用 MDSModelDeploy 工具來部署物件和資料，或是使用模型部署精靈，只部署模型結構。  
  
## <a name="prerequisites"></a>Prerequisites  
 若要執行此程序：  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱 [管理員 &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)，您就可以在群組中加入及移除使用者。  
  
-   模型封裝必須存在，才能供您編輯。 如需詳細資訊，請參閱[部署模型 &#40;Master Data Services&#41;](../master-data-services/deploying-models-master-data-services.md) 和 [使用精靈建立模型部署封裝](../master-data-services/create-a-model-deployment-package-by-using-the-wizard.md)或[使用 MDSModelDeploy 建立模型部署封裝](../master-data-services/create-a-model-deployment-package-by-using-mdsmodeldeploy.md)。  
  
### <a name="to-edit-a-model-deployment-package"></a>若要編輯模型部署封裝  
  
1.  在 MDS 伺服器上的 Windows 檔案總管中，移至 *drive*:\Program Files\Microsoft SQL Server\130\Master Data Services\Configuration。  
  
2.  執行 ModelPackageEditor.exe。  
  
3.  在模型封裝編輯器精靈中，按一下 [瀏覽]，並移至包含套件的資料夾，然後選取套件，再按一下 [開啟]。 按 [下一步] 。  
  
4.  選取這些實體、衍生階層、訂閱檢視或是您想要部署的商務規則。 取消選取您不想要部署的項目。 按 [下一步] 。  
  
5.  驗證要部署之選取項目的清單。 若要變更，請按一下 [上一步]，並重複步驟 4。  
  
6.  按一下 [瀏覽] 移至您想要用來儲存部分套件的資料夾，然後輸入部分套件的檔案名稱 (副檔名為 .pkg)。 按一下 **[儲存]**。  
  
7.  按一下 **[完成]**。  
  
## <a name="next-steps"></a>Next Steps  
  
-   [使用精靈部署模型部署套件](../master-data-services/deploy-a-model-deployment-package-by-using-the-wizard.md)  
  
-   [使用 MDSModelDeploy 部署模型部署封裝](../master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md)  
  
  

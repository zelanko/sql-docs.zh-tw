---
description: 使用精靈建立模型部署封裝
title: 使用 Wizard 建立模型部署套件
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- deployment packages [Master Data Services], creating
- models [Master Data Services], creating a deployment package
- creating packages [Master Data Services]
ms.assetid: b24ec4c2-1378-4c72-ac69-4ec2647030f0
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 7c776d67ebf49e39ae3593d9ac570fe251abb728
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88477070"
---
# <a name="create-a-model-deployment-package-by-using-the-wizard"></a>使用精靈建立模型部署封裝

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  使用 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 模型部署精靈僅建立模型物件的封裝。 如果您需要在套件中包含資料，請參閱 [使用 MDSModelDeploy 建立模型部署封裝](../master-data-services/create-a-model-deployment-package-by-using-mdsmodeldeploy.md)。  
  
## <a name="prerequisites"></a>先決條件  
 若要執行此程序：  
  
-   在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 應用程式中，您必須擁有存取 [系統管理]**** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱系統 [管理員 &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)。  
  
-   模型必須存在，才能建立其封裝。 如需詳細資訊，請參閱[建立模型 &#40;Master Data Services&#41;](../master-data-services/create-a-model-master-data-services.md)。  
  
### <a name="to-create-a-model-deployment-package"></a>若要建立模型部署封裝  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[系統管理]**。  
  
2.  在 [模型檢視]**** 頁面上，從功能表列指向 [系統]****，然後按一下 [部署]****。  
  
3.  按一下 [模型部署精靈]**** 上的 [建立]****。  
  
4.  在 [建立封裝]**** 頁面上，選取 [模型]**** 清單中的模型。  
  
5.  按一下 [下一步]  。  
  
6.  按一下 [下載]  。  
  
7.  儲存檔案。  
  
8.  按一下 [關閉]**** 以關閉精靈。  
  
## <a name="next-steps"></a>後續步驟  
  
-   [使用精靈部署模型部署封裝](../master-data-services/deploy-a-model-deployment-package-by-using-the-wizard.md)  
  
## <a name="see-also"></a>另請參閱  
 [部署模型 &#40;Master Data Services&#41;](../master-data-services/deploying-models-master-data-services.md)  
  
  

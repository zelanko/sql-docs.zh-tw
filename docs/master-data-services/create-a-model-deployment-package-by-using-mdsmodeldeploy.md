---
title: "使用 MDSModelDeploy 建立模型部署套件 | Microsoft Docs"
ms.custom: SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c2687e39-dc20-494f-a707-2aa29f4c329e
caps.latest.revision: "13"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d8a2773d6858d6ede9118c502afc5aac8122b478
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="create-a-model-deployment-package-by-using-mdsmodeldeploy"></a>使用 MDSModelDeploy 建立模型部署封裝
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，使用 MDSModelDeploy 工具來建立封裝。 根據您指定的命令，此封裝可以包含：  
  
-   僅限模型物件。  
  
-   模型物件和資料。  
  
 如果您想要部署只包含模型物件的封裝，您可以在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 應用程式中改用模型部署精靈。 如需詳細資訊，請參閱 [使用精靈建立模型部署封裝](../master-data-services/create-a-model-deployment-package-by-using-the-wizard.md)。  
  
## <a name="prerequisites"></a>必要條件  
 若要執行此程序：  
  
1.  執行 MDSModelDeploy 工作所需的基本權限如下：  
  
    -   與 MDS 組態管理員相同的 Windows 權限 (Windows 管理員)  
  
    -   MDS 資料庫的 DBA 權限。  
  
2.  使用 MDSModelDeploy 工作建立封裝所需的權限如下：  
  
    -   資料模型的 MDS 模型管理員權限。  
  
    -   MDS ImportExport 功能區域權限。  
  
3.  使用 MDSModelDeploy 工作部署模型所需的權限如下：  
  
    -   MDS Explorer 功能權限  
  
    -   MDS 系統管理功能權限。  
  
4.  使用 MDSModelDeploy 工作列出模型所需的權限如下：  
  
    -   MDS Explorer 功能權限  
  
    -   在訂單的資料模型上查看清單中模型的 MDS 模型管理員權限。  
  
 模型必須存在，才能建立其封裝。 如需詳細資訊，請參閱[建立模型 &#40;Master Data Services&#41;](../master-data-services/create-a-model-master-data-services.md)。  
  
 如需詳細資訊，請參閱 [Administrators &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md) (管理員 (Master Data Services))。  
  
### <a name="to-create-a-model-deployment-package-by-using-mdsmodeldeploy"></a>若要使用 MDSModelDeploy 建立模型部署封裝  
  
1.  開啟系統管理員：命令提示字元。  
  
2.  導覽至 MDSModelDeploy.exe 的位置。  
  
    -   如果 MDS 已安裝在預設位置，此檔案會在 *磁碟機*:\Program Files\Microsoft SQL Server\130\Master Data Services\Configuration 中。  
  
    -   如果 MDS 未安裝在預設位置，請搜尋本機電腦中的 MDSModelDeploy.exe。  
  
3.  選擇性。 檢視選項和說明。  
  
    -   若要顯示所有可用的選項，請輸入 `MDSModelDeploy` ，然後按 Enter 鍵。  
  
    -   若要顯示某個選項的説明，請輸入 *，其中* OptionName `MDSModelDeploy help OptionName`是選項的名稱。  
  
4.  選擇性。 如果您有多個 Web 應用程式，請輸入以下命令並按 Enter 鍵，以判斷您要部署的目標服務名稱：  
  
    ```  
    MDSModelDeploy listservices  
    ```  
  
     隨即傳回值的清單，例如 `MDS1, Default Web Site, MDS`。 需要此清單中的第一個值 (此案例中為 `MDS1`)，才能部署模型。  
  
5.  若要建立包含模型物件和資料的封裝，請輸入下列命令，其中 *ModelName*、 *VersionName*、 *ServiceName*和 *PackageName* 分別是模型、版本、服務和 .pkg 輸出檔的名稱：  
  
    ```  
    MDSModelDeploy createpackage -model ModelName -version VersionName -service ServiceName -package PackageName -includedata  
    ```  
  
     如果您不想要包含資料，請勿使用 `-version` 和 `-includedata` 參數。  
  
6.  按 Enter 鍵。 當成功建立封裝之後，隨即顯示一則訊息，表示「MDSModelDeploy 作業已順利完成」。  
  
## <a name="next-steps"></a>後續步驟  
  
-   [使用 MDSModelDeploy 部署模型部署封裝](../master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md)  
  
## <a name="see-also"></a>另請參閱  
 [模型部署選項 &#40;Master Data Services&#41;](../master-data-services/model-deployment-options-master-data-services.md)   
 [部署模型 &#40;Master Data Services&#41;](../master-data-services/deploying-models-master-data-services.md)  
  
  

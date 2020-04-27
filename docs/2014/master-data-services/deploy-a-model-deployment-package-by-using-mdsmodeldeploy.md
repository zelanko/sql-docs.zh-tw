---
title: 使用 MDSModelDeploy 部署模型部署套件 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: fb2a4df4-5e0d-4b34-818f-383dbde1b15c
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 81c87a7990c6c7125cbccbe99050cd5ee477e6d4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "65483077"
---
# <a name="deploy-a-model-deployment-package-by-using-mdsmodeldeploy"></a>使用 MDSModelDeploy 部署模型部署封裝
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，使用 MDSModelDeploy 工具來部署封裝，其中包含下列其中一項：  
  
-   僅限模型物件。  
  
-   模型物件和資料。  
  
 如果您想要部署只包含模型物件的封裝，您可以在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 應用程式中改用模型部署精靈。 如需詳細資訊，請參閱 [使用精靈部署模型部署封裝](../../2014/master-data-services/deploy-a-model-deployment-package-by-using-the-wizard.md)。  
  
> [!IMPORTANT]  
>  封裝只能部署到之前建立封裝所使用的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本。 這表示，在 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 中建立的套件無法部署到 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 或更高版本。  
  
## <a name="prerequisites"></a>先決條件  
 若要執行此程序：  
  
-   在目標 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 環境中，您必須擁有存取 [系統管理]**** 功能區域的權限。  
  
-   模型部署封裝必須存在。 如需詳細資訊，請參閱  [使用 MDSModelDeploy 建立模型部署套件](../../2014/master-data-services/create-a-model-deployment-package-by-using-mdsmodeldeploy.md)。  
  
-   您必須是您要部署模型之環境中的管理員。 如需詳細資訊，請參閱系統[管理員 &#40;Master Data Services&#41;](administrators-master-data-services.md)。  
  
-   如果您要使用資料更新模型，您所部署的版本就無法**鎖定**或**認可**。  
  
### <a name="to-deploy-a-model-deployment-package"></a>若要部署模型部署封裝  
  
1.  決定您要部署新的模型、模型的複製，還是更新之前複製的模型。 如需詳細資訊，請參閱[模型部署選項 &#40;Master Data Services&#41;](../../2014/master-data-services/model-deployment-options-master-data-services.md)。  
  
2.  開啟命令提示字元，並導覽至 MDSModelDeploy.exe。  
  
    -   如果 MDS 已安裝在預設位置，此工具可在*磁片磁碟機*： \PROGRAM Files\Microsoft SQL Server\120\Master Data services\configuration\mdsmodeldeploy.exe 中。中取得。  
  
    -   如果 MDS 未安裝在預設位置，請搜尋本機電腦中的 MDSModelDeploy.exe。  
  
3.  選擇性。 檢視選項和說明。  
  
    -   若要顯示所有可用的選項，請輸入 `MDSModelDeploy` ，然後按 Enter 鍵。  
  
    -   若要顯示某個選項的説明，請輸入 *，其中* OptionName `MDSModelDeploy help OptionName`是選項的名稱。  
  
4.  選擇性。 如果您有多個 Web 應用程式，請輸入以下命令並按 Enter 鍵，以判斷您要部署的目標服務名稱：  
  
    ```  
    MDSModelDeploy listservices  
    ```  
  
     隨即傳回值的清單，例如 `MDS1, Default Web Site, MDS`。 此清單中的第一個值 (此案例中為 `MDS1`) 是部署模型所需的項目。  
  
5.  根據您是建立模型、複製模型還是更新模型，在命令提示字元輸入以下命令並按 Enter 鍵。  
  
    -   若要建立新模型：  
  
        ```  
        MDSModelDeploy deploynew -package PackageName -model ModelName -service ServiceName  
        ```  
  
    -   若要建立模型的複製：  
  
        ```  
        MDSModelDeploy deployclone -package PackageName  
        ```  
  
    -   若要更新現有的模型及其資料：  
  
        ```  
        MDSModelDeploy deployupdate -package PackageName -version VersionName  
        ```  
  
    > [!IMPORTANT]  
    >  如果您使用 MDSModelDeploy 工具來更新現有模型及其資料，而且封裝不包含存在目的地模型中的實體、屬性或成員，MDSModelDeploy 就不會從模型中刪除該實體、屬性或成員。  
  
     其中 *PackageName* 是套件 (.pkg) 檔案的名稱、 *ModelName* 是新模型的名稱、 *VersionName* 是版本的名稱，而 *ServiceName* 是您在上一個步驟傳回的服務名稱。 確定模型和版本名稱符合區分大小寫的精確名稱。  
  
6.  當成功部署套件後，隨即顯示一則訊息，表示「MDSModelDeploy 作業已順利完成」。  
  
 **注意：**  
  
-   如果封裝中的訂閱視圖與現有模型中的訂閱視圖具有相同的名稱，則會將此視圖建立為*modelname. modelname.subscriptionviewname*。 如果此名稱已在使用中，則不會建立訂閱檢視。  
  
-   部署程序有四個步驟：  
  
    1.  建立模型物件。  
  
    2.  建立商務規則。  
  
    3.  建立訂閱檢視。  
  
    4.  擴展主要資料。  
  
-   當建立新的模型或複製的模型時，如果此程序在任何步驟期間失敗，就會刪除該模型。  
  
     更新模型時，如果此程序在前三個步驟期間失敗，就不會繼續進行，但是，並不會回復已經進行的變更。 如果此程序在步驟 4 失敗，則會更新可以更新的成員。  
  
## <a name="next-steps"></a>後續步驟  
 使用者定義的中繼資料、檔案屬性及使用者和群組的權限不包含在模型部署封裝中。 在部署模型之後，您必須手動更新這些項目。 如需詳細資訊，請參閱：  
  
-   [新增中繼資料 &#40;Master Data Services&#41;](../../2014/master-data-services/add-metadata-master-data-services.md)  
  
-   [指派模型物件權限 &#40;Master Data Services&#41;](../../2014/master-data-services/assign-model-object-permissions-master-data-services.md)  
  
## <a name="see-also"></a>另請參閱  
 [部署模型 &#40;Master Data Services&#41;](../../2014/master-data-services/deploying-models-master-data-services.md)  
  
  

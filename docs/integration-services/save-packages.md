---
title: 儲存套件 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.savecopyas.f1
helpviewer_keywords:
- Integration Services packages, saving
- packages [Integration Services], saving
- saving packages
- SSIS packages, saving
- SQL Server Integration Services packages, saving
ms.assetid: 17c1de2c-637f-45c2-a148-79294bae0af4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fb26be1034632ce747c21239636f9b0a4ec08114
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86913264"
---
# <a name="save-packages"></a>儲存封裝

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中，您可以使用 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師來建立封裝，並將封裝儲存為檔案系統中的 XML 檔案 (.dtsx 檔案)。 您也可以將封裝 XML 檔案的複本儲存至 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中的 msdb 資料庫，或儲存至封裝存放區。 封裝存放區代表 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務所管理之檔案系統位置中的資料夾。  
  
 如果您將封裝儲存至檔案系統，可以在稍後使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務將封裝匯入 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 或匯入封裝存放區。 如需詳細資訊，請參閱 [Integration Services Service &#40;SSIS Service&#41;](../integration-services/service/integration-services-service-ssis-service.md) (Integration Services 服務 (SSIS 服務))。  
  
 您也可以使用命令提示字元公用程式 **dtutil**，在檔案系統與 msdb 之間複製封裝。 如需詳細資訊，請參閱 [dtutil Utility](../integration-services/dtutil-utility.md)。  
## <a name="save-a-package-to-the-file-system"></a>將封裝儲存至檔案系統  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟包含您要儲存至檔案的封裝之 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按一下您要儲存的封裝。  
  
3.  在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  
  
    > [!NOTE]  
    >  您可以在 [屬性] 視窗中，確認儲存封裝的路徑和檔案名稱。  

## <a name="save-a-copy-of-a-package"></a>儲存封裝的複本
  本節描述如何將套件複本儲存至檔案系統、套件存放區，或   中的 [!INCLUDE[msCoName](../includes/msconame-md.md)]msdb[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫。 當您指定儲存封裝副本的位置時，也可以更新封裝名稱。  
  
 封裝存放區可以包含 **msdb** 資料庫和檔案系統中的資料夾、或者只有包含 **msdb**，或只有包含檔案系統中的資料夾。 在 **msdb**中，封裝是儲存至 **sysssispackages** 資料表。 這個資料表包含了識別封裝所屬之邏輯資料夾的 **folderid** 資料行。 邏輯資料夾會以相同的方式為 **msdb** 中所儲存的封裝提供實用的分組方法，就像檔案系統中的資料夾為檔案系統中所儲存的封裝提供實用的分組方法一樣。 **msdb** 中 **sysssispackagefolders** 資料表的資料列會定義資料夾。  
  
 如果 **msdb** 不是定義為封裝存放區的一部分，那麼當您在 **[封裝路徑]** 選項中選取 SQL Server 時，可以繼續讓封裝與現有邏輯資料夾產生關聯。  
  
> [!NOTE]  
>  您必須先在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師中開啟封裝，才能儲存封裝的副本。  
  
### <a name="to-save-a-copy-of-a-package"></a>若要儲存封裝的副本  
  
1.  在 [方案總管] 中，按兩下要儲存副本的封裝。  
  
2.  在 [檔案] 功能表上，按一下 [將 \<package file> 的複本另存新檔]。  
  
3.  在 **[儲存封裝的副本]** 對話方塊中，從 **[封裝位置]** 清單選取封裝位置。 有下列選項可供使用：  
    -   SQL Server
    -   檔案系統 
    -   SSIS 封裝存放區 
  
4.  如果位置為 **[SQL Server]** 或 **[SSIS 封裝存放區]** ，請提供伺服器名稱。  
  
5.  若要儲存至 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，請指定驗證類型；如果使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 驗證，請提供使用者名稱與密碼。  
  
6.  若要指定封裝路徑，請輸入路徑或按一下瀏覽按鈕 ([...])  指定封裝的位置。 封裝的預設名稱是 Package。 您也可以選擇更新封裝名稱，以符合您的需求。  
  
     如果您選取 **[SQL Server]** 作為 **[封裝路徑]** 選項，封裝路徑會由 **msdb** 中的邏輯資料夾和封裝名稱組成。 例如，如果 DownloadMonthlyData 封裝與 [MSDB] 資料夾 ( **msdb**中根邏輯資料夾的預設名稱) 中的 [Finance] 資料夾關聯，則名為 DownloadMonthlyData 之封裝的封裝路徑就是 MSDB/Finance/DownloadMonthlyData  
  
     如果您選取 **[SSIS 封裝存放區]** 作為 **[封裝路徑]** 選項，封裝路徑會由 Integration Services 服務所管理的資料夾組成。 例如，如果 UpdateDeductions 封裝位於服務所管理之檔案系統資料夾的 [HumanResources] 資料夾中，封裝路徑就是 /File System/HumanResources/UpdateDeductions；同樣地，如果封裝 PostResumes 是與 [MSDB] 資料夾中的 [HumanResources] 資料夾關聯，封裝路徑就是 MSDB/HumanResources/PostResumes。  
  
     如果您選取 **[檔案系統]** 作為 **[封裝路徑]** 選項，封裝路徑就是檔案系統中的位置和檔案名稱。 例如，如果封裝名稱是 UpdateDemographics，封裝路徑就是 C:\HumanResources\Quarterly\UpdateDemographics.dtsx。  
  
7.  檢閱封裝保護等級。  
  
8.  或者，按一下 [保護等級] 方塊旁的瀏覽按鈕 ([...])，以變更保護等級。  
  
    -   在 **[封裝保護等級]** 對話方塊中，選取不同的保護等級。  
  
    -   按一下 [確定]  。  
  
9. 按一下 [確定]  。  

## <a name="save-a-package-as-a-package-template"></a>將套件儲存為套件範本
 本節描述當您在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中建立新的 Integration Services 套件時，如何指定及使用自訂套件作為範本。 根據預設，當您將新封裝加入 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案中時， [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 會使用可建立空白封裝的封裝範本。 您不能置換這個預設範本，但是可以加入新的範本。  
  
 您可以指定將多個封裝當作範本使用。 不過您必須先建立封裝，才能將自訂封裝實作成範本。  
  
 使用自訂封裝作為範本以建立封裝時，新封裝將擁有與範本相同的名稱和 GUID。 為了區分這些封裝，您應該更新 **Name** 屬性的值，並為 **ID** 屬性產生新的 GUID。 如需詳細資訊，請參閱 [在 SQL Server 資料工具中建立封裝](../integration-services/create-packages-in-sql-server-data-tools.md) 和 [設定封裝屬性](../integration-services/set-package-properties.md)。  
  
### <a name="to-designate-a-custom-package-as-a-package-template"></a>若要將自訂封裝指定成封裝範本  
  
1.  在檔案系統中，尋找要用來當作範本的封裝。  
  
2.  將封裝複製到 DataTransformationItems 資料夾。 依預設，這個資料夾位於 C:\Program Files\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies\ProjectItems\DataTransformationProject。  
  
3.  對想要當作範本使用的每個封裝重複步驟 1 和 2。  
  
### <a name="to-use-a-custom-package-as-a-package-template"></a>若要使用自訂封裝作為封裝範本  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟您要在其中建立封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  在方案總管中，以滑鼠右鍵按一下專案，指向 [加入]  ，然後按一下 [新增項目]  。  
  
3.  在 [新增項目 -\<project name>] 對話方塊中，按一下要當作範本使用的套件。  
  
     範本清單中包含名稱為 [新增 SSIS 封裝] 的預設封裝範本。 封裝圖示識別可當作封裝範本使用的範本。  
  
4.  按一下 [新增]  。  

---
title: 儲存封裝的複本 |Microsoft Docs
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
- Integration Services packages, saving
- packages [Integration Services], saving
- saving packages
- SSIS packages, saving
- SQL Server Integration Services packages, saving
ms.assetid: 21482a20-e420-4452-b7eb-8f9fa1929f31
caps.latest.revision: 23
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 94439ee54ad468af77b89557fa63ad9c108d4f63
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37314158"
---
# <a name="save-a-copy-of-a-package"></a>儲存封裝的複本
  此程序描述如何將封裝的複本儲存至檔案系統、封裝存放區，或  中的 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 當您指定儲存封裝副本的位置時，也可以更新封裝名稱。  
  
 封裝存放區可以包含 **msdb** 資料庫和檔案系統中的資料夾、或者只有包含 **msdb**，或只有包含檔案系統中的資料夾。 在 **msdb**中，封裝是儲存至 **sysssispackages** 資料表。 這個資料表包含了識別封裝所屬之邏輯資料夾的 **folderid** 資料行。 邏輯資料夾會以相同的方式為 **msdb** 中所儲存的封裝提供實用的分組方法，就像檔案系統中的資料夾為檔案系統中所儲存的封裝提供實用的分組方法一樣。 **msdb** 中 **sysssispackagefolders** 資料表的資料列會定義資料夾。  
  
 如果 **msdb** 不是定義為封裝存放區的一部分，那麼當您在 **[封裝路徑]** 選項中選取 SQL Server 時，可以繼續讓封裝與現有邏輯資料夾產生關聯。  
  
> [!NOTE]  
>  您必須先在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師中開啟封裝，才能儲存封裝的副本。  
  
### <a name="to-save-a-copy-of-a-package"></a>若要儲存封裝的副本  
  
1.  在 [方案總管] 中，按兩下要儲存副本的封裝。  
  
2.  在 [檔案] 功能表上，按一下 [另存\<套件檔案> 的副本為]。  
  
3.  在 **[儲存封裝的副本]** 對話方塊中，從 **[封裝位置]** 清單選取封裝位置。  
  
4.  如果位置為 **[SQL Server]** 或 **[SSIS 封裝存放區]**，請提供伺服器名稱。  
  
5.  若要儲存至 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，請指定驗證類型；如果使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 驗證，請提供使用者名稱與密碼。  
  
6.  若要指定封裝路徑，請輸入路徑或按一下瀏覽按鈕 **(…)** 指定封裝的位置。 封裝的預設名稱是 Package。 您也可以選擇更新封裝名稱，以符合您的需求。  
  
     如果您選取 **[SQL Server]** 作為 **[封裝路徑]** 選項，封裝路徑會由 **msdb** 中的邏輯資料夾和封裝名稱組成。 例如，如果 DownloadMonthlyData 封裝與 [MSDB] 資料夾 ( **msdb**中根邏輯資料夾的預設名稱) 中的 [Finance] 資料夾關聯，則名為 DownloadMonthlyData 之封裝的封裝路徑就是 MSDB/Finance/DownloadMonthlyData  
  
     如果您選取 **[SSIS 封裝存放區]** 作為 **[封裝路徑]** 選項，封裝路徑會由 Integration Services 服務所管理的資料夾組成。 例如，如果 UpdateDeductions 封裝位於服務所管理之檔案系統資料夾的 [HumanResources] 資料夾中，封裝路徑就是 /File System/HumanResources/UpdateDeductions；同樣地，如果封裝 PostResumes 是與 [MSDB] 資料夾中的 [HumanResources] 資料夾關聯，封裝路徑就是 MSDB/HumanResources/PostResumes。  
  
     如果您選取 **[檔案系統]** 作為 **[封裝路徑]** 選項，封裝路徑就是檔案系統中的位置和檔案名稱。 例如，如果封裝名稱是 UpdateDemographics，封裝路徑就是 C:\HumanResources\Quarterly\UpdateDemographics.dtsx。  
  
7.  檢閱封裝保護等級。  
  
8.  或者，按一下 [保護等級] 方塊旁的瀏覽按鈕 **(…)**，以變更保護等級。  
  
    -   在 **[封裝保護等級]** 對話方塊中，選取不同的保護等級。  
  
    -   按一下 [確定] 。  
  
9. 按一下 [確定] 。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS&#41;封裝](../../2014/integration-services/integration-services-ssis-packages.md)   
 [設定 Integration Services 服務&#40;SSIS 服務&#41;](service/integration-services-service-ssis-service.md)  
  
  

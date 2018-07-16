---
title: 套件管理 (SSIS 服務) | Microsoft Docs
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
- SQL Server Integration Services packages, managing
- packages [Integration Services], managing
- Integration Services packages, managing
- storing packages
- Stored Packages folder
- current packages
- Running Packages folder
- status information [Integration Services]
- SSIS packages, managing
- storage [Integration Services]
- monitoring [Integration Services], packages
- Integration Services service, package management
- services [Integration Services], package management
ms.assetid: 0261ed9e-3b01-4e37-a9d4-d039c41029b6
caps.latest.revision: 57
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e41b4df0064343cadf6a7da042c243191c0561d6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37172959"
---
# <a name="package-management-ssis-service"></a>封裝管理 (SSIS 服務)
  封裝的管理包含下列工作：  
  
-   監視執行中的封裝  
  
-   管理封裝儲存體  
  
-   匯入和匯出封裝  
  
> [!IMPORTANT]  
>  本主題會討論 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務，即用於管理 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝的 Windows 服務。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 支援此服務能與舊版 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]回溯相容。 從 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]開始，您可以管理 Integration Services 伺服器上的物件，例如封裝。  
  
## <a name="package-store"></a>封裝存放區  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供兩個最上層資料夾用來存取[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]套件： **Running Packages**並**存放的封裝**。 **[Running Packages]** 資料夾會列出伺服器上目前正在執行的封裝。 **[Stored Packages]** 資料夾會列出所有儲存在封裝存放區中的封裝。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務只會管理這些封裝。 封裝存放區可以只由 msdb 資料庫組成，或者由該資料庫和 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務組態檔中所列之檔案系統資料夾所組成。 組態檔會指定要管理的 msdb 及檔案系統資料夾。 您可能還有不是由 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務所管理的封裝，而存放在檔案系統的其他位置。  
  
 您儲存到 msdb 的封裝會存放在名為 sysssispackages 的資料表中。 當您將封裝儲存到 msdb 時，還可以將它們群組成邏輯資料夾。 使用邏輯資料夾可以協助您依用途組織封裝，或是篩選 sysssispackages 資料表中的封裝。 您可以經由使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]建立新的邏輯資料夾。 依預設，您加入至 msdb 的任何邏輯資料夾都會自動納入封裝存放區。  
  
 您在 msdb 中針對群組封裝建立的邏輯資料夾，會呈現為 msdb 中 sysssispackagefolders 資料表的資料列。 sysssispackagefolders 中的 folderid 及 parentfolderid 資料行會定義資料夾階層。 msdb 中的根邏輯資料夾是 sysssispackagefolders 的 parentfolderid 資料行中具有 Null 值的資料列。 如需詳細資訊，請參閱 [sysssispackages &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/sysssispackages-transact-sql) 和 [sysssispackagefolders &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/sysssispackagefolders-transact-sql)。  
  
 當您開啟 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 並連接到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 時，會看到列在 Stored Packages 資料夾中由 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務所管理的 msdb 資料夾。 如果組態檔指定了根檔案系統資料夾，[Stored Packages] 資料夾也會在這些資料夾及所有子資料夾中列出儲存至檔案系統的封裝。  
  
 您可以將封裝存放在任何檔案系統資料夾中，但這些封裝不會列在 **[Stored Packages]** 資料夾的子資料夾中，除非您在組態檔的封裝存放區資料夾清單中加入這個資料夾。 如需組態檔的詳細資訊，請參閱[設定 Integration Services 服務 &#40;SSIS 服務&#41;](integration-services-service-ssis-service.md)。  
  
 **[Running Packages]** 資料夾不包含子資料夾，且不可延伸。  
  
 依預設， **[Stored Packages]** 資料夾包含兩個資料夾： **[File System]** 和 **[MSDB]**。 **[檔案系統]** 資料夾會列出儲存至檔案系統的封裝。 這些檔案的位置是在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務的組態檔中指定的。 預設資料夾為 [封裝] 資料夾，位於 %Program Files%\Microsoft SQL Server\100\DTS。 **MSDB** 資料夾會列出已儲存至伺服器上 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] msdb 資料庫的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 封裝。 sysssispackages 資料表包含 msdb 中所儲存的封裝。  
  
 若要檢視封裝存放區中的封裝清單，您必須開啟 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 並連接到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]。 如需詳細資訊，請參閱 < [SQL Server Management Studio 中檢視 Integration Services 封裝&#40;SSIS 服務&#41;](../view-integration-services-packages-in-sql-server-management-studio-ssis-service.md)。  
  
## <a name="monitoring-running-packages"></a>監視執行中的封裝  
 **[Running Packages]** 資料夾會列出目前正在執行的封裝。 若要在 **的** [摘要] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]頁面上檢視有關目前封裝的資訊，請按一下 **Running Packages** 資料夾。 **[摘要]** 頁面上會列出諸如正在執行封裝的執行持續時間等資訊。 選擇性地重新整理資料夾以顯示最新的資訊。  
  
 若要在 **[摘要]** 頁面上檢視有關單一正在執行封裝的資訊，請按一下該封裝。 **[摘要]** 頁面會顯示諸如封裝的版本和描述等資訊。  
  
 在 [Running Packages] 資料夾中以滑鼠右鍵按一下封裝，然後按一下 [停止]，可以停止正在執行封裝。  
  
## <a name="managing-package-storage"></a>管理封裝儲存體  
 若要組織封裝，您可以將自訂資料夾加入 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務在其組態檔中列出的根封裝存放區資料夾。 依預設，根資料夾為 **[File System]** 和 **[MSDB]** 資料夾。 例如，您可能想要將包含用於清除資料之所有封裝的 **[Data Cleaning]** 資料夾加入 **[File System]** 資料夾。 您可以將自訂資料夾加入自訂資料夾，以建立巢狀資料夾階層來滿足您的需要。 可以刪除和重新命名自訂資料夾，不過，您無法重新命名或刪除組態檔指定的根資料夾。 若要更新 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 列出的根資料夾，您必須更新組態檔。  
  
 如需詳細資訊，請參閱[設定 Integration Services 服務 &#40;SSIS 服務&#41;](../configuring-the-integration-services-service-ssis-service.md)。  
  
## <a name="importing-and-exporting-packages"></a>匯入和匯出封裝  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝可以儲存至 msdb 資料庫或檔案系統。 您可以使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供的匯入或匯出功能，將封裝從一個儲存類型複製到另一個儲存類型。 您還可以將封裝匯入相同的儲存類型，並為封裝指定不同的名稱，藉此建立封裝的複本。 **dtutil** 命令提示字元公用程式 (dtutil.exe) 也可用於匯入及匯出封裝。  
  
 如需詳細資訊，請參閱 [dtutil Utility](../dtutil-utility.md)。  
  
## <a name="related-tasks"></a>相關工作  
  
-   [匯入和匯出封裝&#40;SSIS 服務&#41;](../import-and-export-packages-ssis-service.md)  
  
-   [檢視 Integration Services 封裝，在 SQL Server Management Studio &#40;SSIS 服務&#41;](../view-integration-services-packages-in-sql-server-management-studio-ssis-service.md)  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 服務 &#40;SSIS 服務&#41;](integration-services-service-ssis-service.md)  
  
  

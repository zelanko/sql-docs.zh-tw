---
title: 建立封裝組態 |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Integration Services packages, configurations
- Package Configurations Organizer dialog box
- SSIS packages, configurations
- Integration Services packages, configurations
- configurations [Integration Services]
- packages [Integration Services], configurations
- deploying packages [Integration Services], configurations
ms.assetid: 91ac0347-f908-44f5-bd3d-115790223af4
caps.latest.revision: 71
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ec353414e9b910285152ed3f391ca4dc1970ed45
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37266784"
---
# <a name="create-package-configurations"></a>Create Package Configurations
  使用 [封裝組態組合管理] 對話方塊和「封裝組態精靈」，可以建立封裝組態。 若要存取這些工具，請在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 的 [SSIS] 功能表中，按一下 [封裝組態]。  
  
> [!NOTE]  
>  您也可以按一下 [組態] 屬性旁邊的省略符號按鈕，藉以存取 [封裝組態組合管理]。 [組態] 屬性會顯示在封裝的屬性視窗中。  
  
> [!NOTE]  
>  組態可用於封裝部署模型。 參數是用來取代專案部署模型的組態。 專案部署模型讓您能將 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案部署到 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 伺服器。 如需有關部署模型的詳細資訊，請參閱＜ [Deployment of Projects and Packages](packages/deploy-integration-services-ssis-projects-and-packages.md)＞。  
  
 在 [封裝組態組合管理] 對話方塊中，您可啟用封裝以使用組態、加入和刪除組態，以及設定載入組態的慣用順序。  
  
> [!NOTE]  
>  以喜好的順序載入封裝組態時，組態會根據 **[封裝組態組合管理]** 對話方塊中清單顯示的順序 (由上而下) 依序載入。 不過，在執行階段，封裝組態可能不會以喜好的順序載入。 特別是，父封裝組態會在其他類型的組態後面載入。  
  
> [!NOTE]  
>  如果多個組態設定同一物件屬性，則在執行階段會使用上次載入的值。  
  
 從 [封裝組態組合管理] 對話方塊執行 [封裝組態精靈]，以逐步引導您建立組態。 若要執行 [封裝組態精靈]，請在 [封裝組態組合管理] 對話方塊中加入新的組態，或編輯現有的組態。 在精靈頁面上，選擇組態類型、選取是要直接存取組態還是使用環境變數，並選取要在組態中儲存的屬性。  
  
 下列範例會顯示 [封裝組態精靈] 的 [正在完成精靈] 頁面上所顯示之變數及封裝的目標屬性：  
  
 \Package.Variables[User::TodaysDate].Properties[RaiseChangedEvent]  
  
 \Package.Properties[MaximumErrorCount]  
  
 \Package.Properties[LoggingMode]  
  
 \Package.Properties[LocaleID]  
  
 \Package\My SQL Task.Variables[User::varTableName].Properties[Value]  
  
 在此範例中，此組態會更新以下屬性：  
  
-   使用者定義變數 `TodaysDate`的 RaiseChangedEvent 屬性。  
  
-   封裝的 MaximumErrorCount、LoggingMode 和 LocaleID 屬性。  
  
-   在 My SQL Task 工作範圍內，使用者自訂變數 `varTableName`的 Value 屬性。  
  
 "\Package" 代表根目錄，而句號 (.) 則會分隔物件，這些物件會定義組態所更新之屬性的路徑。 變數及屬性的值是以方括號括住。 不論封裝名稱，組態中一律會使用 Package 這個詞彙；然而，路徑中的所有其他物件都會使用它們的使用者自訂名稱。  
  
 在精靈完成後，新組態會加入 [封裝組態組合管理] 對話方塊中的組態清單。  
  
> [!NOTE]  
>  「封裝組態精靈」的最後一頁，也就是 [正在完成精靈] 頁面，會列出組態中的目標屬性。 如果您想要在執行封裝時使用 **dtexec** 命令提示公用程式來更新屬性，可以執行封裝組態精靈來產生代表屬性路徑的字串，然後再將這些字串複製並貼到命令提示字元視窗中，以便搭配 **dtexec** 的設定選項使用。  
  
 下表描述 [封裝組態組合管理] 對話方塊中組態清單中的資料行。  
  
|「資料行」|描述|  
|------------|-----------------|  
|**組態名稱**|組態的名稱。|  
|**組態類型**|組態類型。|  
|**組態字串**|組態的位置。 此位置可以是路徑、環境變數、登錄機碼、父封裝變數名稱或 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫中的資料表。|  
|**目標物件**|具有擁有組態之屬性的物件名稱。 如果組態為 XML 組態檔，則資料行是空白的，因為該組態可更新多個物件。|  
|**目標屬性**|屬性的名稱。 如果組態寫入 XML 組態檔或 SQL Server 資料表，則資料行是空白的，因為該組態可更新多個物件。|  
  
### <a name="to-create-a-package-configuration"></a>建立封裝組態  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  在 [[!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師] 中，按一下 [控制流程]、[資料流程]、[事件處理常式] 或 [封裝總管] 索引標籤。  
  
4.  在 [SSIS] 功能表上，按一下 [封裝組態]。  
  
5.  在 [封裝組態組合管理] 對話方塊中，選取 [啟用封裝組態]，然後按一下 [加入]。  
  
6.  在 [封裝組態精靈] 頁面的歡迎頁面上，按 [下一步]。  
  
7.  在 [選取組態類型] 頁面上，指定組態類型，然後設定與組態類型相關聯的屬性。 如需詳細資訊，請參閱[封裝組態精靈 UI 參考](../../2014/integration-services/package-configuration-wizard-ui-reference.md)。  
  
8.  在 [選取要匯出的屬性] 頁面上，選取要併入組態之封裝物件的屬性。 如果組態類型僅支援一個屬性，此精靈頁面的標題將為 [選取目標屬性]。 如需詳細資訊，請參閱[封裝組態精靈 UI 參考](../../2014/integration-services/package-configuration-wizard-ui-reference.md)。  
  
    > [!NOTE]  
    >  只有 [XML 組態檔] 和 [SQL Server] 組態類型支援在組態中併入多個屬性。  
  
9. 在 [正在完成精靈] 頁面上，輸入組態的名稱，然後按一下 [完成]。  
  
10. 檢視 [封裝組態組合管理] 對話方塊中的組態。  
  
11. 按一下 [ **關閉**]。  
  
## <a name="external-resources"></a>外部資源  
  
-   msdn.microsoft.com 上的技術文件： [了解 Integration Services 封裝組態](http://go.microsoft.com/fwlink/?LinkId=165643)  
  
-   www.sqlis.com 上的部落格文章： [Creating packages in code – Package Configurations](http://go.microsoft.com/fwlink/?LinkId=217663)(透過程式碼建立封裝 – 封裝組態)。  
  
-   blogs.msdn.com 上的部落格文章： [API Sample – Programmatically add a configuration file to a package](http://go.microsoft.com/fwlink/?LinkId=217664)(API 範例 - 以程式設計方式將組態檔加入封裝中)。  
  
## <a name="see-also"></a>另請參閱  
 [封裝組態](../../2014/integration-services/package-configurations.md)   
 [封裝部署&#40;SSIS&#41;](packages/legacy-package-deployment-ssis.md)   
 [以程式設計方式使用變數](building-packages-programmatically/working-with-variables-programmatically.md)  
  
  

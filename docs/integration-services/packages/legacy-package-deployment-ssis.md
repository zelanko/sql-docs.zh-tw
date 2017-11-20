---
title: "舊版封裝部署 (SSIS) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: packages
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.packageconfigurationorganizer.f1
- sql13.dts.configwizard.finishdtsconfiguration.f1
- sql13.dts.configwizard.selectobjects.f1
- sql13.dts.configwizard.selecconfigtype.f1
- sql13.dts.configwizard.welcome.f1
- sql13.dts.deploymentwizard.welcome.f1
- sql13.dts.deploymentwizard.confirminstallation.f1
- sql13.dts.deploymentwizard.deploydtspackages.f1
- sql13.dts.deploymentwizard.finish.f1
- sql13.dts.deploymentwizard.configurepackages.f1
- sql13.dts.deploymentwizard.selectinstfolder.f1
- sql13.dts.deploymentwizard.packagevalidation.f1
- sql13.dts.deploymentwizard.specifytargetsqlserver.f1
helpviewer_keywords:
- Integration Services packages, deploying
- deploying packages [Integration Services]
- SQL Server Integration Services packages, deploying
- deploying packages [Integration Services], about deploying packages
- packages [Integration Services], deploying
- SSIS packages, deploying
ms.assetid: 0f5fc7be-e37e-4ecd-ba99-697c8ae3436f
caps.latest.revision: 46
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 15c21ac27069d582a7006c38993f48dc3f4ed0be
ms.contentlocale: zh-tw
ms.lasthandoff: 09/27/2017

---
# <a name="legacy-package-deployment-ssis"></a>舊版封裝部署 (SSIS)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含的工具和精靈可以簡化將封裝從開發電腦部署到實際伺服器或部署到其他電腦的流程。  
  
 封裝部署處理有四個步驟：  
  
1.  第一個選擇性的步驟是選擇性的，包含建立可在執行階段更新封裝元素屬性的封裝組態。 部署封裝時，會自動包含這些組態。  
  
2.  第二步是建立 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案，以建立封裝部署公用程式。 專案的部署公用程式包含您要部署的封裝  
  
3.  第三步是將建立 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案時所建立的部署資料夾複製到目標電腦。  
  
4.  第四步是在目標電腦上執行 [封裝安裝精靈]，將封裝安裝到檔案系統或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的執行個體。  

## <a name="package-configurations"></a>封裝組態
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供可用以在執行階段更新屬性值的封裝組態。  
  
> **注意** ：組態可用於套件部署模型。 參數是用來取代專案部署模型的組態。 專案部署模型讓您能將 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器。 如需有關部署模型的詳細資訊，請參閱＜ [Deployment of Projects and Packages](https://msdn.microsoft.com/library/hh213290.aspx)＞。   
  
 組態是您加入已完成封裝的一組屬性/值配對。 一般而言，您建立封裝、在封裝開發期間設定封裝物件的屬性，然後將組態加入至封裝。 當封裝執行時，它會從組態取得新的屬性值； 舉例來說，經由使用組態，您可以變更連接管理員的連接字串，或更新變數的值。  
  
 封裝組態提供下列優點：  
  
-   組態會使將封裝從開發環境移至實際執行環境更為容易。 例如，組態可以更新來源檔案的路徑，或者變更資料庫或伺服器的名稱。  
  
-   組態在您將封裝部署到許多不同的伺服器時非常有用。 例如，組態中每個已部署封裝的變數都可包含不同的磁碟空間值，如果可用磁碟空間不符合這個值，封裝就不會執行。  
  
-   組態使封裝更有彈性。 例如，組態可以更新屬性運算式中使用的變數值。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 支援使用幾種不同的方法儲存封裝組態，例如 XML 檔案、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中的資料表，以及環境和封裝變數。  
  
 每個組態都是屬性/值配對。 XML 組態檔和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態類型可以包含多重組態。  
  
 當您建立用以安裝封裝的封裝部署公用程式時，會包含這些組態。 在安裝封裝時，您可以在封裝的安裝過程中更新這些組態。  
  
### <a name="understanding-how-package-configurations-are-applied-at-run-time"></a>了解如何在執行階段套用封裝組態  
 當您使用 **dtexec** 命令提示字元公用程式 (dtexec.exe) 來執行部署的封裝時，此公用程式會套用封裝組態兩次。 當此公用程式套用您在命令列上所指定之選項的前後，都會套用組態。  
  
 當此公用程式載入及執行此封裝時，事件會依照下列順序發生：  
  
1.  **dtexec** 公用程式會載入此封裝。  
  
2.  此公用程式會套用您在設計階段於封裝內所指定的組態，而且會依照封裝內所指定的順序 (唯一的例外是父封裝變數組態。 此公用程式只會在稍後於處理序中套用這些組態一次)。  
  
3.  然後此公用程式會套用您在命令列上所指定的任何選項。  
  
4.  然後此公用程式會重新載入您在設計階段於封裝內所指定的組態，而且會依照封裝內所指定的順序 (同樣地，此規則的例外是父封裝變數組態)。 此公用程式會使用您所指定的任何命令列選項來重新載入組態。 因此，可能會從不同的位置重新載入不同的值。  
  
5.  此公用程式會套用父封裝變數組態。  
  
6.  此公用程式會執行此封裝。  
  
 **dtexec** 公用程式套用組態的方式會影響下列命令列選項：  
  
-   您可以在執行階段使用 **/Connection** 或 **/Set** 選項，從不同於設計時所指定的位置載入封裝組態。  
  
-   您可以使用 **/ConfigFile** 選項來載入您並未在設計階段指定的其他組態。  
  
 但是，這些命令列選項確實有一些限制：  
  
-   您不能使用 **/Set** 或 **/Connection** 選項來覆寫同樣由組態所設定的單一值。  
  
-   您不能使用 **/ConfigFile** 選項來載入可取代您在設計階段指定之組態的組態。  
  
 如需這些選項的詳細資訊，以及這些選項在 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 與舊版之間的行為差異，請參閱 [SQL Server 2016 中 Integration Services 功能的行為變更](http://msdn.microsoft.com/library/611d22fa-5ac7-485e-9a40-7131e852f794)。  
  
### <a name="package-configuration-types"></a>封裝組態類型  
 下表描述封裝組態類型。  
  
|型別|說明|  
|----------|-----------------|  
|XML 組態檔|XML 檔案包含組態。 XML 檔案可以包含多重組態。|  
|環境變數|環境變數包含組態。|  
|登錄項目|登錄項目包含組態。|  
|父封裝變數|封裝中的變數包含組態。 這個組態類型通常用來更新子封裝中的屬性。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] table|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中的資料表包含組態。 資料表可以包含多重組態。|  
  
#### <a name="xml-configuration-files"></a>XML 組態檔  
 如果選取 [XML 組態檔] 組態類型，您可以建立新的組態檔、重複使用現有的檔案並加入新組態，或者重複使用現有的檔案但覆寫現有的檔案內容。  
  
 XML 組態檔包含兩個區段：  
  
-   包含組態檔相關資訊的標題。 此元素包含諸如檔案建立時間和產生檔案之使用者的姓名等屬性。  
  
-   包含每個組態相關資訊的組態項目。 此元素包含諸如屬性 (Property) 路徑和屬性 (Property) 的已設定值等屬性 (Attribute)。  
  
 下面的 XML 程式碼會示範 XML 組態檔的語法。 這個範例會示範名為 `MyVar`之整數變數的 Value 屬性組態。  
  
```xml
\<?xml version="1.0"?>  
<DTSConfiguration>  
   <DTSConfigurationHeading>  
      <DTSConfigurationFileInfo  
          GeneratedBy="DomainName\UserName"  
          GeneratedFromPackageName="Package"  
          GeneratedFromPackageID="{2AF06766-817A-4E28-9878-0DE37A150648}"  
          GeneratedDate="2/01/2005 5:58:09 PM"/>  
   </DTSConfigurationHeading>  
   <Configuration ConfiguredType="Property" Path="\Package.Variables[User::MyVar].Value" ValueType="Int32">  
      <ConfiguredValue>0</ConfiguredValue>  
   </Configuration>  
</DTSConfiguration>  
  
```  
  
#### <a name="registry-entry"></a>登錄項目  
 如果您想使用登錄項目儲存組態，可以使用現有的機碼或在 HKEY_CURRENT_USER 中建立新的機碼。 您所使用的登錄機碼必須具有名為 **Value**的值。 該值可以是 DWORD 或字串。  
  
 如果您選取 [登錄項目] 組態類型，就要在 [登錄項目] 方塊中輸入登錄機碼的名稱。 格式是\<登錄機碼 >。 如果您想要使用不在 HKEY_CURRENT_USER 根目錄的登錄機碼，使用格式\<y key>\\...> 若要找出的金鑰。 例如，若要使用位於 SSISPackages 中的 MyPackage 機碼，請輸入 **SSISPackages\MyPackage**。  
  
#### <a name="sql-server"></a>SQL Server  
 如果選取 [SQL Server] 組態類型，則需要指定要儲存組態之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫的連接。 您可以將組態儲存至現有的資料表，或者在指定的資料庫中建立新的資料表。  
  
 下列 SQL 陳述式顯示 [封裝組態精靈] 提供的預設 CREATE TABLE 陳述式。  
  
```sql
CREATE TABLE [dbo].[SSIS Configurations]  
(  
ConfigurationFilter NVARCHAR(255) NOT NULL,  
ConfiguredValue NVARCHAR(255) NULL,  
PackagePath NVARCHAR(255) NOT NULL,  
ConfiguredValueType NVARCHAR(20) NOT NULL  
)  
  
```  
  
 您提供給組態的名稱為 **ConfigurationFilter** 資料行中儲存的值。  
  
### <a name="direct-and-indirect-configurations"></a>直接和間接組態  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供直接和間接組態。 如果您直接指定組態， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 便會在組態項目和封裝物件屬性之間建立直接的連結。 來源的位置沒有變更時，使用直接組態是較好的選擇。 例如，如果您確定封裝中的所有部署都使用相同的檔案路徑，便可指定 XML 組態檔。  
  
 間接組態會使用環境變數。 與直接指定組態設定的方法不同，間接組態會指向包含組態值的環境變數。 如果組態的位置可以針對封裝的每個部署變更，則使用間接組態是較好的選擇。  

## <a name="create-package-configurations"></a>Create Package Configurations
  使用 [套件組態組合管理] 對話方塊和 [套件組態精靈]，可以建立套件組態。 若要存取這些工具，請在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 的 [SSIS] 功能表中，按一下 [封裝組態]。  
  
  
 **注意：**
>您按一下**組態**屬性旁邊的省略符號按鈕，也可以存取 [套件組態組合管理]。 [組態] 屬性會顯示在封裝的屬性視窗中。  
  
>組態可用於封裝部署模型。 參數是用來取代專案部署模型的組態。 專案部署模型讓您能將 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器。 如需有關部署模型的詳細資訊，請參閱＜ [Deployment of Projects and Packages](https://msdn.microsoft.com/library/hh213290.aspx)＞。    
  
>在 [封裝組態組合管理] 對話方塊中，您可啟用封裝以使用組態、加入和刪除組態，以及設定載入組態的慣用順序。 
 
>以喜好的順序載入封裝組態時，組態會根據 **[封裝組態組合管理]** 對話方塊中清單顯示的順序 (由上而下) 依序載入。 不過，在執行階段，封裝組態可能不會以喜好的順序載入。 特別是，父封裝組態會在其他類型的組態後面載入。  
  
>如果多個組態設定同一物件屬性，則在執行階段會使用上次載入的值。  
  
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
  
> **注意：**[套件組態精靈] 的最後一頁，也就是 [正在完成精靈] 頁面，會列出組態中的目標屬性。 如果您想要在執行封裝時使用 **dtexec** 命令提示公用程式來更新屬性，可以執行封裝組態精靈來產生代表屬性路徑的字串，然後再將這些字串複製並貼到命令提示字元視窗中，以便搭配 **dtexec** 的設定選項使用。  
  
 下表描述 [封裝組態組合管理] 對話方塊中組態清單中的資料行。  
  
|資料行|說明|  
|------------|-----------------|  
|**組態名稱**|組態的名稱。|  
|**組態類型**|組態類型。|  
|**組態字串**|組態的位置。 此位置可以是路徑、環境變數、登錄機碼、父封裝變數名稱或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中的資料表。|  
|**目標物件**|具有擁有組態之屬性的物件名稱。 如果組態為 XML 組態檔，則資料行是空白的，因為該組態可更新多個物件。|  
|**目標屬性**|屬性的名稱。 如果組態寫入 XML 組態檔或 SQL Server 資料表，則資料行是空白的，因為該組態可更新多個物件。|  
  
### <a name="to-create-a-package-configuration"></a>建立封裝組態  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  在 [[!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師] 中，按一下 [控制流程]、[資料流程]、[事件處理常式] 或 [封裝總管] 索引標籤。  
  
4.  在 [SSIS] 功能表上，按一下 [封裝組態]。  
  
5.  在 封裝組態組合管理 對話方塊中，選取 啟用封裝組態，然後按一下加入。  
  
6.  在 [封裝組態精靈] 頁面的歡迎頁面上，按 [下一步]。  
  
7.  在 [選取組態類型] 頁面上，指定組態類型，然後設定與組態類型相關聯的屬性。 如需詳細資訊，請參閱 [封裝組態精靈 UI 參考](../../integration-services/packages/package-configuration-wizard-ui-reference.md)。  
  
8.  在 [選取要匯出的屬性] 頁面上，選取要併入組態之封裝物件的屬性。 如果組態類型僅支援一個屬性，此精靈頁面的標題將為 [選取目標屬性]。 如需詳細資訊，請參閱[封裝組態精靈 UI 參考](../../integration-services/packages/package-configuration-wizard-ui-reference.md)。  
  
    > **注意：**只有 [XML 組態檔] 和 [SQL Server] 組態類型支援在組態中併入多個屬性。  
  
9. 在 正在完成精靈 頁面上，輸入組態的名稱，然後按一下完成。  
  
10. 檢視 [封裝組態組合管理] 對話方塊中的組態。  
  
11. 按一下 [ **關閉**]。  

## <a name="package-configurations-organizer"></a>[封裝組態組合管理]
  使用 **[封裝組態組合管理]** 對話方塊，即可啟用封裝組態、檢視目前封裝的組態清單，以及指定載入組態的喜好順序。  
  
> **注意** ：組態可用於套件部署模型。 參數是用來取代專案部署模型的組態。 專案部署模型讓您能將 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器。 如需有關部署模型的詳細資訊，請參閱＜ [Deployment of Projects and Packages](https://msdn.microsoft.com/library/hh213290.aspx)＞。    
  
 如果組態更新相同的屬性，列於組態清單較下面的組態值會取代清單中較上面的組態值。 載入屬性的最後一個值是封裝執行時所使用的值。 此外，如果封裝使用如 XML 組態檔案等直接組態以及如環境變數等間接組態的組合，則指向直接組態位置的間接組態必須是清單中較上面的部份。  
  
> **注意**：以喜好的順序載入套件組態時，組態會根據 [套件組態組合管理] 對話方塊中清單顯示的順序 (由上而下) 依序載入。 不過，在執行階段，封裝組態可能不會以喜好的順序載入。 特別是，父封裝組態會在其他類型的組態後面載入。  
  
 封裝組態會在執行階段更新封裝物件的屬性值。 載入封裝時，組態值將會取代開發封裝時所設定的值。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 支援不同的組態類型。 例如，您可以使用包含多個組態的 XML 檔案，或是包含單一組態的環境變數。 如需相關資訊，請參閱 [Package Configurations](../../integration-services/packages/package-configurations.md)。  
  
### <a name="options"></a>選項。  
 **啟用封裝組態**  
 選取即可使用封裝的組態。  
  
 **組態名稱**  
 檢視組態的名稱。  
  
 **組態類型**  
 檢視儲存組態的位置類型。  
  
 **組態字串**  
 檢視儲存組態值的位置。 位置可以是檔案的路徑、環境變數的名稱、父封裝變數的名稱、登錄機碼，或是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表的名稱。  
  
 **目標物件**  
 檢視組態所更新之物件的名稱。 如果組態是 XML 組態檔或 SQL Server 資料表，則資料行是空白的，因為該組態可包含多個物件。  
  
 **目標屬性**  
 檢視組態所修改之屬性的名稱。 如果組態類型支援多個組態，則此資料行是空白。  
  
 **加入**  
 使用封裝組態精靈來加入組態。  
  
 **編輯**  
 重新執行封裝組態精靈來編輯現有的組態。  
  
 **移除**  
 選取組態，然後按一下移除。  
  
 **箭頭**  
 選取組態，然後使用向上和向下箭頭，即可將其在清單中向上移動或向下移動。 組態會依其出現在清單中的順序載入。  

## <a name="package-configuration-wizard-ui-reference"></a>封裝組態精靈 UI 參考
  使用 **[封裝組態精靈]** ，即可建立在執行階段更新 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝及其物件之屬性的組態。 當您在 **[封裝組態組合管理]** 對話方塊中加入新的組態或修改現有的組態時，這個精靈便會執行 若要開啟 **[封裝組態組合管理]** 對話方塊，請在 **中選取** [SSIS] **功能表上的** [封裝組態] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]。 如需詳細資訊，請參閱 [建立封裝組態](../../integration-services/packages/create-package-configurations.md)。  
  
> **注意** ：組態可用於套件部署模型。 參數是用來取代專案部署模型的組態。 專案部署模型讓您能將 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器。 如需有關部署模型的詳細資訊，請參閱＜ [Deployment of Projects and Packages](https://msdn.microsoft.com/library/hh213290.aspx)＞。  
  
 下列章節描述精靈頁面。  
  
### <a name="welcome-to-the-package-configuration-wizard-page"></a>歡迎使用封裝組態精靈頁面  
 使用 **[SSIS 組態精靈]** ，即可建立在執行階段更新封裝及其物件之屬性的組態。  
  
#### <a name="options"></a>選項。  
 **不要再顯示此頁面**  
 下次開啟精靈時略過歡迎頁面。  
  
 **下一個**  
 移至精靈的下一個頁面。  
  
### <a name="select-configuration-type-page"></a>選取組態類型頁面  
 使用 **[選取組態類型]** 頁面，即可指定要建立的組態類型。  
  
 如果需要其他資訊才可決定要使用的組態類型，請參閱＜ [Package Configurations](../../integration-services/packages/package-configurations.md)＞。  
  
#### <a name="static-options"></a>靜態選項  
 **組態類型**  
 使用下列選項，即可選取儲存組態的來源類型：  
  
|Value|說明|  
|-----------|-----------------|  
|**XML 組態檔**|將組態儲存為 XML 檔案。 選取這個值就會顯示 **[組態類型]**區段中的動態選項。|  
|**環境變數**|將組態儲存在其中一個環境變數中。 選取這個值就會顯示 **[組態類型]**區段中的動態選項。|  
|**登錄項目**|將組態儲存在登錄中。 選取這個值就會顯示 **[組態類型]**區段中的動態選項。|  
|**父封裝變數**|以變數將組態儲存在包含工作的封裝中。  選取這個值就會顯示 **[組態類型]**區段中的動態選項。|  
|**SQL Server**|將組態儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的資料表中。 選取這個值就會顯示 **[組態類型]**區段中的動態選項。|  
  
 **下一個**  
 檢視精靈順序的下一頁。  
  
#### <a name="dynamic-options"></a>動態選項  
  
##### <a name="configuration-type-option--xml-configuration-file"></a>組態類型選項 = XML 組態檔  
 **直接指定組態設定**  
 這可用來直接指定設定。  
  
|Value|說明|  
|-----------|-----------------|  
|**組態檔名稱**|鍵入精靈產生之組態檔的路徑。|  
|**瀏覽**|使用 **[選取組態檔位置]** 對話方塊，即可指定精靈產生之組態檔的路徑。 如果檔案不存在，精靈就會建立檔案。|  
  
 **組態位置儲存在環境變數中**  
 這可用來指定儲存組態的環境變數。  
  
|Value|說明|  
|-----------|-----------------|  
|**環境變數**|從清單中選取環境變數。|  
  
##### <a name="configuration-type-option--environment-variable"></a>組態類型選項 = 環境變數  
 **環境變數**  
 選取包含組態資訊的環境變數。  
  
##### <a name="configuration-type-option--registry-entry"></a>組態類型選項 = 登錄項目  
 **直接指定組態設定**  
 這可用來直接指定設定。  
  
|Value|說明|  
|-----------|-----------------|  
|**登錄項目**|輸入包含組態資訊的登錄機碼。 格式是\<登錄機碼 >。<br /><br /> 登錄機碼必須已經存在於 HKEY_CURRENT_USER 中且具有名為 Value 的值。 該值可以是 DWORD 或字串。<br /><br /> 如果您想要使用的登錄機碼不是在 HKEY_CURRENT_USER 根目錄中，使用格式\<y key>\\...> 若要找出的金鑰。|  
  
 **組態位置儲存在環境變數中**  
 這可用來指定儲存組態的環境變數。  
  
|Value|說明|  
|-----------|-----------------|  
|**環境變數**|從清單中選取環境變數。|  
  
##### <a name="configuration-type-option--parent-package-variable"></a>組態類型選項 = 父封裝變數  
 **直接指定組態設定**  
 這可用來直接指定設定。  
  
|Value|說明|  
|-----------|-----------------|  
|**父變數**|在包含組態資訊的父封裝中指定變數。|  
  
 **組態位置儲存在環境變數中**  
 這可用來指定儲存組態的環境變數。  
  
|Value|說明|  
|-----------|-----------------|  
|**環境變數**|從清單中選取環境變數。|  
  
##### <a name="configuration-type-options--sql-server"></a>組態類型選項 = SQL Server  
 **直接指定組態設定**  
 這可用來直接指定設定。  
  
|Value|說明|  
|-----------|-----------------|  
|**連接**|請從清單中選取連接，或按一下 **[新增]** 即可建立新的連接。|  
|**組態資料表**|選取現有的資料表，或按一下 **[新增]** ，即可撰寫建立新資料表的 SQL 陳述式。|  
|**組態篩選**|選取現有的組態名稱或鍵入新的名稱。<br /><br /> 許多 SQL Server 組態可儲存在相同的資料表中，且每個組態都可包括多個組態項目。<br /><br /> 這個使用者自訂值是儲存在資料表中，以識別特定組態所屬的組態項目。|  
  
 **組態位置儲存在環境變數中**  
 這可用來指定儲存組態的環境變數。  
  
|Value|說明|  
|-----------|-----------------|  
|**環境變數**|從清單中選取環境變數。|  
  
### <a name="select-objects-to-export-page"></a>選取要匯出的物件頁面  
 使用 **[選取目標屬性] 或 [選取要匯出的屬性]** 頁面，即可指定組態包含的物件屬性。 只有選取 XML 組態類型時，才能選取多個屬性。  
  
#### <a name="options"></a>選項。  
 **物件**  
 展開封裝階層，並選取要匯出的屬性。  
  
 **Property 屬性**  
 檢視屬性 (property) 的屬性 (attribute)。  
  
 **下一個**  
 移至精靈的下一頁。  
  
### <a name="completing-the-wizard-page"></a>正在完成精靈頁面  
 使用 **[正在完成精靈]** 頁面，即可提供組態的名稱，並檢視精靈用來建立組態的設定。 在精靈完成之後，就會顯示 **[封裝組態組合管理]** ，其中會列出封裝的所有組態。  
  
#### <a name="options"></a>選項。  
 **組態名稱**  
 鍵入組態的名稱。  
  
 **預覽**  
 檢視精靈用來建立組態的設定。  
  
 **[完成]**  
 建立組態，並結束 [封裝組態精靈]。  

## <a name="child"></a>子封裝中使用變數和參數的值
  此程序描述如何建立使用父變數組態類型的封裝組態。 此組態類型可讓從父封裝執行的子封裝存取父變數。  
  
> [!NOTE]  
>  您也可以設定 [執行封裝工作] 將父封裝變數或參數 (或專案參數) 對應到子封裝參數，以將值傳遞到子封裝。 如需詳細資訊，請參閱 [執行封裝工作](../../integration-services/control-flow/execute-package-task.md)。  
  
 在子封裝中建立封裝組態之前，並不需要在父封裝中建立變數。 您可以隨時將變數加入父封裝中，但是必須使用封裝組態中父變數的確切名稱。 不過，在可以更新組態的子封裝中必須包含現有的變數，您才可以建立父變數組態。 如需加入和設定變數的詳細資訊，請參閱 [加入、刪除、變更封裝中使用者定義變數的範圍](http://msdn.microsoft.com/library/cbf40c7f-3c8a-48cd-aefa-8b37faf8b40e)。  
  
 父變數組態使用之父封裝中變數的範圍可以設定為「執行封裝」工作、擁有該工作的容器，或是封裝。 如果封裝中定義了多個名稱相同的變數，則會使用最接近「執行封裝」工作範圍的變數。 最接近「執行封裝」工作的範圍就是工作本身。  
  
### <a name="to-add-a-variable-to-a-parent-package"></a>若要將變數加入父封裝  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含要加入用來傳遞到子封裝之變數的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  在 [[!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師] 中，若要定義變數的範圍，請執行下列其中之一：  
  
    -   若要將範圍設為封裝，請按一下 [控制流程] 索引標籤之設計介面上的任意位置。  
  
    -   若要將範圍設定為「執行封裝」工作的父容器，請按一下該容器。  
  
    -   若要將範圍設定為「執行封裝」，請按一下該工作。  
  
4.  加入及設定變數。  
  
    > [!NOTE]  
    >  選取與變數所要儲存之資料相容的資料類型。  
  
5.  若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  
  
### <a name="to-add-a-variable-to-a-child-package"></a>若要將變數加入子封裝  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含要加入父變數組態之封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中，若要將範圍設定為封裝，請按一下 [控制流程] 索引標籤之設計介面上的任意位置。  
  
4.  加入及設定變數。  
  
    > [!NOTE]  
    >  選取與變數所要儲存之資料相容的資料類型。  
  
5.  若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  

## <a name="create-a-deployment-utility"></a>Create a Deployment Utility
  部署封裝的第一步是建立 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案的部署公用程式。 部署公用程式是一個資料夾，包含在其他伺服器的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案中部署封裝所需的檔案。 部署公用程式在儲存 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案的電腦上建立。  
  
 建立 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案之封裝部署公用程式的方法是先設定建立部署公用程式的建立程序，然後再建立專案。 建立專案時，會自動併入專案中所有的封裝和封裝組態。 若要部署專案的其他檔案 (例如讀我檔案)，請將檔案放置在 **專案的** [Miscellaneous] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 資料夾中。 建立專案時，會自動併入這些檔案。  
  
 您可以不同的方式設定每一個專案部署。 在建立專案和建立封裝部署公用程式之前，您可以設定部署公用程式上的屬性，以自訂在專案中部署封裝的方式。 例如，可以指定在部署專案時是否可以更新封裝組態。 若要存取 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案的屬性，請以滑鼠右鍵按一下專案，然後按一下 [屬性]。  
  
 下表列出部署公用程式屬性。  
  
|屬性|說明|  
|--------------|-----------------|  
|AllowConfigurationChange|指定部署期間是否可以更新組態的值。|  
|[CreateDeploymentUtility]|指定建立專案時是否建立封裝部署公用程式的值。 此屬性必須為 **True** ，才能建立部署公用程式。|  
|DeploymentOutputPath|與部署公用程式之 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案相關的位置。|  
  
 當您建置[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]專案時，資訊清單檔\<專案名稱 >。C t Name>.ssisdeploymentmanifest.xml，建立並新增，以及專案封裝和封裝相依性，在專案中的 bin\Deployment 資料夾或 DeploymentOutputPath 屬性中指定的位置的複本。 資訊清單檔會列出專案中的封裝、封裝組態和任何其他檔案。  
  
 每次建立專案時，都會重新整理部署資料夾的內容。 這表示系統將會刪除儲存在這個資料夾，而建立程序並未重新複製到資料夾中的任何檔案。 例如，儲存在部署資料夾的封裝組態檔案將會被刪除。  
  
### <a name="to-create-a-package-deployment-utility"></a>建立封裝部署公用程式  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含要為其建立封裝部署公用程式之 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案的方案。  
  
2.  以滑鼠右鍵按一下專案，然後按一下 [屬性]。  
  
3.  在**\<專案名稱 > 屬性頁**對話方塊中，按一下 **部署公用程式**。  
  
4.  若要在部署封裝時更新封裝組態，請將 **[AllowConfigurationChanges]** 設為 **True**。  
  
5.  將 **[CreateDeploymentUtility]** 設為 **True**。  
  
6.  選擇性地修改 **DeploymentOutputPath** 屬性，以更新部署公用程式的位置。  
  
7.  按一下 **[確定]**。  
  
8.  在方案總管中，以滑鼠右鍵按一下專案，然後按一下建立。  
  
9. 檢視 **[輸出]** 視窗中的建立進度和建立錯誤。  

## <a name="deploy-packages-by-using-the-deployment-utility"></a>Deploy Packages by Using the Deployment Utility
  當已建立部署公用程式，以從建立部署公用程式之電腦以外電腦上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案安裝封裝時，必須首先將部署資料夾複製到目的地電腦。  
  
 部署資料夾的路徑是在為其建立部署公用程式之 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案的 DeploymentOutputPath 屬性中指定的。 預設路徑為 bin\Deployment (相對於 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案)。 如需詳細資訊，請參閱 [建立部署公用程式](../../integration-services/packages/create-a-deployment-utility.md)。  
  
 請使用「封裝安裝精靈」來安裝封裝。 若要啟動此精靈，請在將部署資料夾複製到伺服器後按兩下部署公用程式檔案。 這個檔案命名為\<專案名稱 >。SSISDeploymentManifest，以及可以在目的地電腦上，部署資料夾中找到。  
  
> [!NOTE]  
>  根據所部署的封裝版本，如果有不同版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 並存安裝，可能會發生錯誤。 因為 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]所有版本的 .SSISDeploymentManifest 副檔名都相同，所以可能會發生這項錯誤。 按兩下此檔案就會針對最近安裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]版本 (可能與部署公用程式檔案的版本不同) 呼叫安裝程式 (dtsinstall.exe)。 若要解決此問題，請從命令列執行正確的 dtsinstall.exe 版本，並且提供部署公用程式檔案的路徑。  
  
 [封裝安裝精靈] 會逐步引導您將封裝安裝到檔案系統或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 您可以利用下列方式來設定安裝：  
  
-   選擇用來安裝封裝的位置類型和位置。  
  
-   選擇用來安裝封裝相依性的位置。  
  
-   在封裝安裝在目標伺服器之後驗證封裝。  
  
 封裝之以檔案作為基礎的相依性總是安裝到檔案系統。 如果您將封裝安裝到檔案系統，則會將相依性安裝到為封裝指定的資料夾。 如果您將封裝安裝到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，則可指定要儲存以檔案基礎之相依性的資料夾。  
  
 如果封裝包含您要修改以用於目的地電腦的組態，則可使用精靈更新屬性的值。  
  
 除了使用 [封裝安裝精靈] 安裝封裝之外，還可以使用 **dtutil** 命令提示字元公用程式來複製和移動封裝。 如需詳細資訊，請參閱 [dtutil Utility](../../integration-services/dtutil-utility.md)。  
  
### <a name="to-deploy-packages-to-an-instance-of-sql-server"></a>將封裝部署至 SQL Server 的執行個體  
  
1.  開啟目標電腦上的部署資料夾。  
  
2.  按兩下資訊清單檔\<專案名稱 >。SSISDeploymentManifest，啟動 封裝安裝精靈。  
  
3.  在 [部署 SSIS 封裝] 頁面上，選取 [SQL Server 部署] 選項。  
  
4.  選擇性地選取 [安裝之後驗證封裝]，以在將封裝安裝到目標伺服器後對其進行驗證。  
  
5.  在 [指定目標 SQL Server] 頁面上，指定要安裝封裝的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體，並選取驗證模式。 如果選取「[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證」，則您必須提供使用者名稱和密碼。  
  
6.  在 [選取安裝資料夾] 頁面上，為要安裝的封裝相依性指定檔案系統中的資料夾。  
  
7.  如果封裝包括組態，則可透過更新 [設定封裝] 頁面上 [值] 清單中的值來編輯組態。  
  
8.  如果選擇在安裝後驗證封裝，請檢視已部署封裝的驗證結果。  

## <a name="redeployment-of-packages"></a>封裝的重新部署
  在部署專案後，您可能需要更新或擴充封裝功能，然後部署包含已更新封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。 做為重新部署封裝處理的一部分，您應該檢視包含在部署公用程式中的組態屬性。 例如，您可能不允許組態在重新部署封裝之後變更。  
  
### <a name="process-for-redeployment"></a>重新部署程序  
 在封裝更新完成後，您會重新建置專案、將部署資料夾複製到目標電腦，然後傳回 [封裝安裝精靈]。  
  
 如果您只更新專案中的幾個封裝，則可能不想重新部署整個專案。 若要只部署幾個封裝，您可以建立新的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案、將已更新的封裝加入新的專案，然後建立和部署該專案。 當您將封裝加入其他專案時，封裝組態會自動隨封裝一同複製。  

## <a name="package-installation-wizard-ui-reference"></a>封裝安裝精靈 UI 參考
  使用 [封裝安裝精靈] 來部署 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案，包括其內含的封裝和其他檔案，以及任何封裝的相依性。  
  
 在部署封裝之前，可以建立組態，然後將其隨封裝部署。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會使用組態，在執行階段以動態方式更新封裝及封裝物件的屬性。 例如，OLE DB 連接的連接字串可提供對應值與包含連接字串屬性的組態，藉此於執行階段進行動態設定。  
  
 您必須先建置 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案並建立部署公用程式，才能執行 [封裝安裝精靈]。 如需詳細資訊，請參閱 [使用部署公用程式來部署封裝](../../integration-services/packages/deploy-packages-by-using-the-deployment-utility.md)。  
  
 下列章節描述精靈頁面。  
  
### <a name="welcome-to-the-package-installation-wizard-page"></a>歡迎使用封裝安裝精靈頁面  
 使用 [封裝安裝精靈]，即可部署建立了封裝部署公用程式的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  
  
 **不要再顯示此開始頁面**  
 選取再次執行精靈時要略過開始頁面。  
  
 **下一個**  
 移至精靈的下一頁。  
  
 **完成**  
 跳到 [完成封裝安裝精靈] 頁面。 如果您依序返回精靈的頁面以修訂您的選擇，並且指定了所有必要的選項，則請使用這個選項。  
  
### <a name="configure-packages-page"></a>設定封裝頁面  
 使用 [設定封裝] 頁面即可編輯封裝組態。  
  
#### <a name="options"></a>選項。  
 **組態檔**  
 從清單中選取檔案來編輯組態檔的內容。  
  
 **相關主題：**[建立封裝組態](../../integration-services/packages/create-package-configurations.md)  
  
 **路徑**  
 檢視要設定之屬性的路徑。  
  
 **型別**  
 檢視屬性的資料類型。  
  
 **Value**  
 指定組態的值。  
  
 **下一個**  
 移至精靈的下一頁。  
  
 **完成**  
 跳到 [完成封裝安裝精靈] 頁面。 如果您依序返回精靈的頁面以修訂您的選擇，並且指定了所有必要的選項，則請使用這個選項。  
  
### <a name="confirm-installation-page"></a>確認安裝頁面  
 使用 [確認安裝] 頁面，即可開始安裝封裝、檢視狀態，以及檢視精靈用以從指定專案中安裝檔案的資訊。  
  
 **下一個**  
 安裝封裝及其相依檔案，並在安裝完成時移到下一個精靈頁面。  
  
 **狀態**  
 顯示封裝安裝的進度。  
  
 **完成**  
 移至 [完成封裝安裝精靈] 頁面。 如果您有回到先前的精靈頁面來修改選擇，並且指定了所有必要的選項，請使用此選項。  
  
### <a name="deploy-ssis-packages-page"></a>部署 SSIS 封裝頁面  
 使用 [部署 SSIS 封裝] 頁面，來指定安裝 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝及其相依性的位置。  
  
#### <a name="options"></a>選項。  
 **檔案系統部署**  
 將封裝及相依性部署到檔案系統的指定資料夾中。  
  
 **SQL Server 部署**  
 將封裝及相依性部署到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的執行個體中。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在伺服器之間共用封裝，請使用此選項。 所有的封裝相依性都會安裝到檔案系統的指定資料夾中。  
  
 **安裝之後驗證封裝**  
 指出是否在安裝之後驗證封裝。  
  
 **下一個**  
 移至精靈的下一頁。  
  
 **完成**  
 跳到 [完成封裝安裝精靈] 頁面。 如果您依序返回精靈的頁面以修訂您的選擇，並且指定了所有必要的選項，則請使用這個選項。  
  
### <a name="packages-validation-page"></a>封裝驗證頁面  
 使用 [封裝驗證] 頁面，即可檢視封裝驗證的進度與結果。  
  
 **下一個**  
 移至精靈的下一頁。  
  
### <a name="select-installation-folder-page"></a>選取安裝資料夾頁面  
 使用 [選取安裝資料夾] 頁面，即可指定安裝封裝及其相依性的檔案系統資料夾。  
  
#### <a name="options"></a>選項。  
 **資料夾**  
 指定複製封裝及其相依性的路徑和資料夾。  
  
 **瀏覽**  
 使用 [瀏覽資料夾] 對話方塊，即可瀏覽至目標資料夾。  
  
 **下一個**  
 移至精靈的下一頁。  
  
 **完成**  
 跳到 [完成封裝安裝精靈] 頁面。 如果您有依序返回精靈的其他頁面以修訂選擇，並且已指定了所有必要的選項，則請使用此選項。  
  
### <a name="specify-target-sql-server-page"></a>指定目標 SQL Server 頁面  
 使用 [指定目標 SQL Server] 頁面，即可指定將封裝部署至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的選項。  
  
#### <a name="options"></a>選項。  
 **伺服器名稱**  
 指定部署封裝目的地之伺服器的名稱。  
  
 **使用 Windows 驗證**  
 指定是否使用 Windows 驗證來登入伺服器。 建議使用 Windows 驗證，以獲得較佳的安全性。  
  
 **使用 SQL Server 驗證**  
 指定封裝是否應使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證來登入伺服器。 如果您使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證，就必須提供使用者名稱和密碼。  
  
 **使用者名稱**  
 指定使用者名稱。  
  
 **密碼**  
 指定密碼。  
  
 **封裝路徑**  
 指定邏輯資料夾名稱，或輸入 "/" 代表預設資料夾。  
  
 若要在 [SSIS 封裝] 對話方塊中選取資料夾，請按一下 [瀏覽 (...)]。不過，此對話方塊並不能用來選取預設資料夾。 如果想要使用預設資料夾，必須在文字方塊中輸入 "/"。  
  
> [!NOTE]  
>  如果沒有輸入有效的封裝路徑，則會出現下列錯誤訊息：「有一些引數無效。」  
  
 **依賴伺服器儲存體進行加密**  
 選取即可使用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的安全性功能來保護封裝的安全。  
  
 **下一個**  
 移至精靈的下一頁。  
  
 **完成**  
 跳到 [完成封裝安裝精靈] 頁面。 如果您依序返回精靈的頁面以修訂您的選擇，並且指定了所有必要的選項，則請使用這個選項。  
  
### <a name="finish-the-package-installation-page"></a>完成封裝安裝頁面  
 使用 [完成封裝安裝精靈] 頁面，即可檢視封裝安裝結果的摘要。 此頁面提供詳細資料，例如已部署的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案、已安裝的封裝、組態檔以及安裝位置。  
  
 **[完成]**  
 按一下 [完成] 以結束精靈。  



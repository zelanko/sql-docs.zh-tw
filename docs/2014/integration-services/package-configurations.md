---
title: 封裝組態 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- package configuration syntax [Integration Services]
- SQL Server Integration Services packages, configurations
- SSIS packages, configurations
- XML [Integration Services]
- Integration Services packages, configurations
- configuration syntax [Integration Services]
- indirect configurations [Integration Services]
- configurations [Integration Services]
- direct configurations [Integration Services]
- packages [Integration Services], configurations
ms.assetid: d20e0311-1fc9-4ddc-a381-6d127cf11b69
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 832cd038151c3816decbc17542c805ed7e161465
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48200918"
---
# <a name="package-configurations"></a>封裝組態
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 提供封裝組態可供您在執行階段更新屬性的值。  
  
> [!NOTE]  
>  組態可用於封裝部署模型。 參數是用來取代專案部署模型的組態。 專案部署模型讓您能將 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案部署到 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 伺服器。 如需有關部署模型的詳細資訊，請參閱＜ [部署專案和封裝](packages/deploy-integration-services-ssis-projects-and-packages.md)＞。  
  
 組態是您加入已完成封裝的一組屬性/值配對。 一般而言，您建立封裝、在封裝開發期間設定封裝物件的屬性，然後將組態加入至封裝。 當封裝執行時，它會從組態取得新的屬性值； 舉例來說，經由使用組態，您可以變更連接管理員的連接字串，或更新變數的值。  
  
 封裝組態提供下列優點：  
  
-   組態會使將封裝從開發環境移至實際執行環境更為容易。 例如，組態可以更新來源檔案的路徑，或者變更資料庫或伺服器的名稱。  
  
-   組態在您將封裝部署到許多不同的伺服器時非常有用。 例如，組態中每個已部署封裝的變數都可包含不同的磁碟空間值，如果可用磁碟空間不符合這個值，封裝就不會執行。  
  
-   組態使封裝更有彈性。 例如，組態可以更新屬性運算式中使用的變數值。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 支援數個不同的方法儲存封裝組態，例如 XML 檔案、 資料表中[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]資料庫以及環境和封裝變數。  
  
 每個組態都是屬性/值配對。 XML 組態檔和 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 組態類型可以包含多重組態。  
  
 當您建立用以安裝封裝的封裝部署公用程式時，會包含這些組態。 在安裝封裝時，您可以在封裝的安裝過程中更新這些組態。  
  
## <a name="understanding-how-package-configurations-are-applied-at-run-time"></a>了解如何在執行階段套用封裝組態  
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
  
 如需有關這些選項，以及這些選項的行為之間的差異[!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)]和舊版中，請參閱[SQL Server 2014 中 Integration Services 功能的行為變更](../../2014/integration-services/behavior-changes-to-integration-services-features-in-sql-server-2014.md)。  
  
## <a name="package-configuration-types"></a>封裝組態類型  
 下表描述封裝組態類型。  
  
|類型|描述|  
|----------|-----------------|  
|XML 組態檔|XML 檔案包含組態。 XML 檔案可以包含多重組態。|  
|環境變數|環境變數包含組態。|  
|登錄項目|登錄項目包含組態。|  
|父封裝變數|封裝中的變數包含組態。 這個組態類型通常用來更新子封裝中的屬性。|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料表|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫中的資料表包含組態。 資料表可以包含多重組態。|  
  
### <a name="xml-configuration-files"></a>XML 組態檔  
 如果選取 [XML 組態檔] 組態類型，您可以建立新的組態檔、重複使用現有的檔案並加入新組態，或者重複使用現有的檔案但覆寫現有的檔案內容。  
  
 XML 組態檔包含兩個區段：  
  
-   包含組態檔相關資訊的標題。 此元素包含諸如檔案建立時間和產生檔案之使用者的姓名等屬性。  
  
-   包含每個組態相關資訊的組態項目。 此元素包含諸如屬性 (Property) 路徑和屬性 (Property) 的已設定值等屬性 (Attribute)。  
  
 下面的 XML 程式碼會示範 XML 組態檔的語法。 這個範例會示範名為 `MyVar`之整數變數的 Value 屬性組態。  
  
```  
<?xml version="1.0"?>  
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
  
### <a name="registry-entry"></a>登錄項目  
 如果您想使用登錄項目儲存組態，可以使用現有的機碼或在 HKEY_CURRENT_USER 中建立新的機碼。 您使用的登錄機碼值必須是名為`Value`。 該值可以是 DWORD 或字串。  
  
 如果您選取 [登錄項目] 組態類型，就要在 [登錄項目] 方塊中輸入登錄機碼的名稱。 格式為 \<登錄機碼>。 如果您想要使用不是在 HKEY_CURRENT_USER 根目錄的登錄機碼，請使用 \<登錄機碼\登錄機碼\\...> 格式識別該機碼。 例如，若要使用位於 SSISPackages 中的 MyPackage 機碼，請輸入`SSISPackages\MyPackage`。  
  
### <a name="sql-server"></a>[SQL Server]  
 如果選取 [SQL Server] 組態類型，則需要指定要儲存組態之 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫的連接。 您可以將組態儲存至現有的資料表，或者在指定的資料庫中建立新的資料表。  
  
 下列 SQL 陳述式顯示 [封裝組態精靈] 提供的預設 CREATE TABLE 陳述式。  
  
```  
CREATE TABLE [dbo].[SSIS Configurations]  
(  
ConfigurationFilter NVARCHAR(255) NOT NULL,  
ConfiguredValue NVARCHAR(255) NULL,  
PackagePath NVARCHAR(255) NOT NULL,  
ConfiguredValueType NVARCHAR(20) NOT NULL  
)  
  
```  
  
 您提供給組態的名稱為 **ConfigurationFilter** 資料行中儲存的值。  
  
## <a name="direct-and-indirect-configurations"></a>直接和間接組態  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 提供直接和間接組態。 如果您直接指定組態，[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 便會在組態項目和封裝物件屬性之間建立直接的連結。 來源的位置沒有變更時，使用直接組態是較好的選擇。 例如，如果您確定封裝中的所有部署都使用相同的檔案路徑，便可指定 XML 組態檔。  
  
 間接組態會使用環境變數。 與直接指定組態設定的方法不同，間接組態會指向包含組態值的環境變數。 如果組態的位置可以針對封裝的每個部署變更，則使用間接組態是較好的選擇。  
  
## <a name="related-tasks"></a>相關工作  
 [建立套件設定](../../2014/integration-services/create-package-configurations.md)  
  
## <a name="related-content"></a>相關內容  
  
-   msdn.microsoft.com 上的技術文件： [Understanding Integration Services Package Configurations](http://go.microsoft.com/fwlink/?LinkId=165643)(了解 Integration Services 封裝組態)  
  
-   www.sqlis.com 上的部落格文章： [Creating packages in code – Package Configurations](http://go.microsoft.com/fwlink/?LinkId=217663)(透過程式碼建立封裝 – 封裝組態)。  
  
-   blogs.msdn.com 上的部落格文章： [API Sample – Programmatically add a configuration file to a package](http://go.microsoft.com/fwlink/?LinkId=217664)(API 範例 - 以程式設計方式將組態檔加入封裝中)。  
  
  

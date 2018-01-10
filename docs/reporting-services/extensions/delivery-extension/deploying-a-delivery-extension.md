---
title: "部署傳遞延伸模組 | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: extensions
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- delivery extensions [Reporting Services], deploying
- Extension element
- deploying [Reporting Services], extensions
ms.assetid: 4436ce48-397d-42c7-9b5d-2a267e2a1b2c
caps.latest.revision: "45"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ac89e662415b74bab2003af1462453ad96b369b1
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2018
---
# <a name="deploying-a-delivery-extension"></a>部署傳遞延伸模組
  傳遞延伸模組以 XML 組態檔的形式提供其組態資訊。 XML 檔案符合為傳遞延伸模組定義的 XML 結構描述。 傳遞延伸模組提供設定和修改組態檔的基礎結構。  
  
 如果取代或升級傳遞延伸模組，則所有參考傳遞延伸模組的訂閱仍然會有效。  
  
 在您將 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 傳遞延伸模組撰寫和編譯成 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 程式庫之後，必須將延伸模組複製到適當的目錄，並將項目新增至適當的 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 設定檔，這樣報表伺服器就可以找到它。  
  
## <a name="configuration-file-extension-element"></a>組態檔延伸模組元素  
 部署到報表伺服器的傳遞延伸模組，需要在設定檔中輸入成 **Extension** 項目。 報表伺服器的組態檔是 RSReportServer.config。  
  
 下表說明傳遞延伸模組之 **Extension** 項目的屬性。  
  
|attribute|描述|  
|---------------|-----------------|  
|**名稱**|延伸模組的唯一名稱 (例如，供電子郵件傳遞延伸模組使用的 "Report Server E-Mail"，或是供檔案共用傳遞延伸模組使用的 "Report Server FileShare")。 **Name** 屬性的最大長度為 255 個字元。 該名稱在組態檔之 **Extension** 元素的所有元素中，必須是唯一的。 如果重複的名稱存在，報表伺服器會傳回錯誤。|  
|**型別**|以逗號分隔的清單，包括完整的命名空間以及組件的名稱。|  
|**Visible**|**false** 值指出在使用者介面中應該看不到傳遞延伸模組。 如果沒有包括屬性，預設值是 **true**。|  
  
 如需 RSReportServer.config 或 RSReportDesigner.config 檔的詳細資訊，請參閱 [Reporting Services 設定檔](../../../reporting-services/report-server/reporting-services-configuration-files.md)。  
  
## <a name="deploying-the-extension-to-the-report-server"></a>將延伸模組部署到報表伺服器  
 報表伺服器使用傳遞延伸模組來處理和傳遞通知或是報表。 您應該將傳遞延伸模組組件部署到報表伺服器做為私用組件， 也需要在報表伺服器組態檔 RSReportServer.config 中建立項目。  
  
#### <a name="to-deploy-a-deliver-extension-assembly-to-a-report-server"></a>將傳遞延伸模組組件部署到報表伺服器  
  
1.  將組件從執行位置複製到您要在其上使用傳遞延伸模組之報表伺服器的 bin 目錄。 報表伺服器 Bin 目錄的預設位置是 %ProgramFiles%\Microsoft SQL Server\MSRS13.\<InstanceName>\Reporting Services\ReportServer\bin。  
  
    > [!IMPORTANT]  
    >  如果您嘗試覆寫現有的傳遞延伸模組件，必須先停止報表伺服器服務，再複製更新的組件。 在組件完成複製之後，重新啟動服務。  
  
2.  在複製組件檔之後，開啟 RSReportServer.config 檔。 RSReportServer.config 檔案位於 %ProgramFiles%\Microsoft SQL Server\MSRS13.\<執行個體名稱>\Reporting Services\ReportServer 目錄。 您需要在傳遞延伸模組組件檔的組態檔中建立項目。 您可以利用 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 或簡單的文字編輯器 (如 [記事本]) 開啟設定檔。  
  
3.  在 RSReportServer.config 檔中，找出 **Delivery** 項目。 應該針對您新建立的傳遞延伸模組，在下列位置建立項目：  
  
    ```  
    <Extensions>  
       <Delivery>  
          <Your extension configuration information goes here>  
       </Delivery>  
    </Extensions>  
    ```  
  
4.  針對您的傳遞延伸模組加入項目。 您的項目應該包含具有 **Name** 和 **Type** 值的 **Extension** 項目，且看起來可能如下所示：  
  
    ```  
    <Extension Name="My Delivery Extension Name" Type="CompanyName.ExtensionName.MyDeliveryExtensionClass, AssemblyName" />  
    ```  
  
     **Name** 的值是傳遞延伸模組的唯一名稱。 **Type** 的值是以逗號分隔的清單，包括實作 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension> 介面之類別的完整命名空間項目，後面接著組件的名稱 (不包含 .dll 副檔名)。 依預設，傳遞延伸模組是可見的。 若要在使用者介面中隱藏延伸模組 (例如入口網站)，請將 **Visible** 屬性新增到 **Extension** 項目，並將其設定為 **false**。  
  
5.  最後，針對為傳遞延伸模組授與 **FullTrust** 權限的自訂組件，新增程式碼群組。 這項作業的進行方式是將程式碼群組新增至 rssrvpolicy.config 檔案，這個檔案預設位於 %ProgramFiles%\Microsoft SQL Server\MSRS13.\<執行個體名稱>\Reporting Services\ReportServer。 您的程式碼群組可能如下所示：  
  
    ```  
    <CodeGroup class="UnionCodeGroup"  
       version="1"  
       PermissionSetName="FullTrust"  
       Name="MyExtensionCodeGroup"  
       Description="Code group for my delivery extension">  
          <IMembershipCondition class="UrlMembershipCondition"  
             version="1"  
             Url="C:\Program Files\Microsoft SQL Server\MSRS13.<InstanceName>\Reporting Services\ReportServer\bin\MyExtensionAssembly.dll"  
           />  
    </CodeGroup>  
    ```  
  
     URL 成員資格僅是您可以針對傳遞延伸模組所選擇的許多成員資格條件的其中一個。 如需 [!INCLUDE[ssRS](../../../includes/ssrs-md.md)] 程式碼存取安全性的詳細資訊，請參閱[安全開發 &#40;Reporting Services&#41;](../../../reporting-services/extensions/secure-development/secure-development-reporting-services.md)  
   
## <a name="verifying-the-deployment"></a>確認部署  
 您可以使用 Web 服務 <xref:ReportService2010.ReportingService2010.ListExtensions%2A> 方法來確認傳遞延伸模組是否已成功部署到報表伺服器。 您也可以開啟入口網站，然後確認延伸模組是否包含在訂閱的可用傳遞延伸模組清單。 如需入口網站及訂用帳戶的詳細資訊，請參閱[訂閱與傳遞 &#40;Reporting Services&#41;](../../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)。  
  
## <a name="see-also"></a>另請參閱  
 [實作傳遞延伸模組](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services 延伸模組程式庫](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  

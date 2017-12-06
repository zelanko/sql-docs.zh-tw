---
title: "部署轉譯延伸模組 | Microsoft Docs"
ms.custom: 
ms.date: 03/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: extensions
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- deploying [Reporting Services], extensions
- rendering extensions [Reporting Services], deploying
ms.assetid: 9fb8c887-5cb2-476e-895a-7b0e2dd11398
caps.latest.revision: "44"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 4121274d43473df5dbf0f8f556b6d3da78ed735a
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="deploying-a-rendering-extension"></a>部署轉譯延伸模組
  在您撰寫 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 報表轉譯延伸模組並將其編譯成 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 程式庫之後，需要使其可供報表伺服器和報表設計師探索。 若要這樣做，請將延伸模組複製到適當的目錄，並將項目加入適當的 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 組態檔。  
  
## <a name="configuration-file-rendering-extension-element"></a>組態檔轉譯延伸模組元素  
 在將轉譯延伸模組編譯成 .DLL 之後，您就可以將項目加入至 rsreportserver.config 檔案。 預設位置為 %ProgramFiles%\Microsoft SQL Server\MSRS10_50.\<執行個體名稱>\Reporting Services\ReportServer。 父項目是 \<Render>。 Render 元素之下是代表每個轉譯延伸模組的 Extension 元素。 **Extension** 元素包含兩個屬性：Name 與 Type。  
  
 下表描述轉譯延伸模組之 **Extension** 元素的屬性：  
  
|Attribute|說明|  
|---------------|-----------------|  
|**名稱**|延伸模組的唯一名稱。 **Name** 屬性的最大長度為 255 個字元。 該名稱在組態檔之 **Extensions** 元素的所有項目中，必須是唯一的。 如果重複的名稱存在，報表伺服器會傳回錯誤。|  
|**型別**|以逗號分隔的清單，包括完整的命名空間以及組件的名稱。|  
|**Visible**|值若為 **false** 表示轉譯延伸模組不應該顯示在使用者介面中。 如果沒有包括屬性，預設值是 **true**。|  
|**LogAllExecutionRequests**|值若為 **false** 表示只會針對工作階段中的第一項報表執行作業記錄項目。 如果沒有包括屬性，預設值是 **true**。<br /><br /> 例如，這項設定會決定只針對報表中轉譯的第一個頁面記錄項目 (當此值為 **false**時)，還是針對報表中轉譯的每個頁面記錄項目 (當此值為 **true**時)。|  
  
 如需詳細資訊，請參閱 [RsReportServer.config 組態檔](../../../reporting-services/report-server/rsreportserver-config-configuration-file.md)。  
  
## <a name="deploying-the-extension-to-the-report-server"></a>將延伸模組部署到報表伺服器  
 報表伺服器會使用轉譯延伸模組將報表匯出成其他格式。 您應該將轉譯延伸模組組件部署到報表伺服器做為私用組件。 也需要在報表伺服器組態檔 rsreportserver.config 中建立項目。  
  
### <a name="to-deploy-the-assembly"></a>若要部署組件  
  
1.  將組件從執行位置複製到您要在其上使用轉譯延伸模組之報表伺服器的 bin 目錄。 報表伺服器 Bin 目錄的預設位置是 %ProgramFiles%\Microsoft SQL Server\MSRS10_50.\<執行個體名稱>\Reporting Services\ReportServer\Bin。  
  
2.  在複製組件檔之後，開啟 rsreportserver.config 檔。 rsreportserver.config 檔也位於報表伺服器的 bin 目錄中。 您需要在延伸模組組件檔的組態檔中建立項目。 您可以利用 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 或簡單的文字編輯器開啟此檔案。  
  
     如需詳細資訊，請參閱 [RsReportServer.config 組態檔](../../../reporting-services/report-server/rsreportserver-config-configuration-file.md)。  
  
3.  在 Rsreportserver.config 檔中，找出 **Render** 元素。 應該針對您新建立的延伸模組，在下列位置建立項目：  
  
    ```  
    <Extensions>  
       <Render>  
          <extension configuration>  
       </Render>  
    </Extensions>  
    ```  
  
4.  針對您的傳遞延伸模組加入項目。 您的項目應該包含具有 **Name** 和 **Type**值的元素，且看起來可能如下所示：  
  
    ```  
    <Extension Name="My Rendering Extension Name" Type="CompanyName.ExtensionName.MyRenderingProvider, AssemblyName" />  
    ```  
  
     **Name** 值是轉譯延伸模組的唯一名稱。 **類型**的值是以逗號分隔的清單，包括 <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension> 實作的完整命名空間項目，後面接著組件的名稱 (不包括 .dll 副檔名)。 根據預設，轉譯延伸模組是可見的。 若要在使用者介面中隱藏延伸模組 (例如報表管理員)，請將 **Visible** 屬性加入到 **Extension** 元素，並將其設定為 **false**。  
  
## <a name="verifying-the-deployment"></a>確認部署  
 您也可以開啟報表管理員，然後確認延伸模組是否包含在報表可用匯出類型的清單中。  
  
## <a name="see-also"></a>另請參閱  
 [實作轉譯延伸模組](../../../reporting-services/extensions/rendering-extension/implementing-a-rendering-extension.md)   
 [轉譯延伸模組概觀](../../../reporting-services/extensions/rendering-extension/rendering-extensions-overview.md)   
 [實作 IRenderingExtension 介面](../../../reporting-services/extensions/rendering-extension/implementing-the-irenderingextension-interface.md)   
 [延伸模組的安全性考量](../../../reporting-services/extensions/security-considerations-for-extensions.md)  
  
  

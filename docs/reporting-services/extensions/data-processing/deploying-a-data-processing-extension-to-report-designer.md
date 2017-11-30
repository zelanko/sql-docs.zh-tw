---
title: "如何：將資料處理延伸模組部署到報表設計師 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- data processing extensions [Reporting Services], deploying
- assemblies [Reporting Services], data processing extension deployments
ms.assetid: 3614e601-004e-4a16-8388-836ffd67e9dd
caps.latest.revision: "41"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 73283dc22ee011a4f02f38a49cdfd6fa67e97cf2
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="deploying-a-data-processing-extension-to-report-designer"></a>將資料處理延伸模組部署到報表設計師
  報表設計工具在您設計報表時，使用資料處理延伸模組來擷取和處理資料。 您應該將資料處理延伸模組組件部署到報表設計師做為私用組件， 您也需要在報表設計師組態檔 RSReportDesigner.config 中建立項目。  
  
#### <a name="to-deploy-a-data-processing-extension-assembly"></a>部署資料處理延伸模組組件  
  
1.  將組件從您的執行位置複製到報表設計師目錄。 報表設計師目錄的預設位置是 C:\Program Files\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies。  
  
2.  在複製組件檔之後，開啟 RSReportDesigner.config 檔。 RSReportDesigner.config 檔案也位於 Report Designer 目錄中。 您需要在資料處理延伸模組組件檔案的組態檔中建立項目。 您可以利用 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 或簡單的文字編輯器 (如 [記事本]) 開啟設定檔。  
  
3.  在 RSReportDesigner.config 檔中，找出 **Data** 元素。 應該針對您新建立的資料處理延伸模組，在下列位置建立項目：  
  
    ```  
    <Extensions>  
       <Data>  
          <Your extension configuration information goes here>  
       </Data>  
    </Extensions>  
    ```  
  
4.  為您的資料處理延伸模組新增一個項目，其中包含具有 **Name**、**Type** 和 **Visible** 屬性值的 **Extension** 項目。 您的輸入可能如下所示：  
  
    ```  
    <Extension Name="ExtensionName" Type="CompanyName.ExtensionName.MyConnectionClass, AssemblyName" />  
    ```  
  
     **Name** 的值是資料處理延伸模組的唯一名稱。 **Type** 的值是以逗號分隔的清單，包括實作 <xref:Microsoft.ReportingServices.Interfaces.IExtension> 和 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection> 介面之類別的完整命名空間項目，後面接著組件的名稱 (不包含 .dll 副檔名)。 依預設值，資料處理延伸模組是可見的。 若要在使用者介面中隱藏延伸模組 (例如報表設計師)，請將 **Visible** 屬性新增至 **Extension** 項目，並將其設定為 **false**。  
  
5.  最後，針對為延伸模組授與 **FullTrust** 權限的自訂組件，新增程式碼群組。 完成此動作的方法是，將程式碼群組加入預設位於 C:\Program Files\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies 中的 rspreviewpolicy.config 檔案。 您的程式碼群組可能如下所示：  
  
    ```  
    <CodeGroup class="UnionCodeGroup"  
       version="1"  
       PermissionSetName="FullTrust"  
       Name="MyExtensionCodeGroup"  
       Description="Code group for my data processing extension">  
          <IMembershipCondition class="UrlMembershipCondition"  
             version="1"  
             Url="C:\Program Files\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies\MyExtensionAssembly.dll"  
           />  
    </CodeGroup>  
    ```  
  
 URL 成員資格僅是您可以針對資料處理延伸模組所選擇的許多成員資格條件的其中一個。 如需 [!INCLUDE[ssRSversion2005](../../../includes/ssrsversion2005-md.md)] 程式碼存取安全性的詳細資訊，請參閱[安全開發 &#40;Reporting Services&#41;](../../../reporting-services/extensions/secure-development/secure-development-reporting-services.md)  
  
## <a name="generic-query-designer"></a>一般查詢設計工具  
 報表設計師提供可和自訂資料處理延伸模組搭配使用的一般查詢設計師。 這個設計工具包含兩個窗格：查詢窗格和結果窗格。 您可以使用一般設計師來撰寫圖形化介面支援的查詢。 和圖形化查詢設計工具不同的是，一般查詢設計工具不會檢查查詢語法或重新設定查詢的結構。  
  
#### <a name="to-enable-the-generic-query-designer-for-a-custom-extension"></a>啟用自訂延伸模組的一般查詢設計工具。  
  
-   將下列查詢新增至 **Designer** 項目之下的 RSReportDesigner.config 檔中，以便使用在之前項目中所提供的名稱來取代 **Name** 屬性。  
  
    ```  
    <Extension Name="ExtensionName" Type="Microsoft.ReportingServices.QueryDesigners.GenericQueryDesigner,Microsoft.ReportingServices.QueryDesigners"/>  
    ```  
  
## <a name="verifying-the-deployment"></a>確認部署  
 在您可以確認部署之前，必須在本機電腦上，關閉 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 的所有執行個體。 在您已經結束所有目前的工作階段後，您可以確認是否已將您的資料處理延伸模組成功部署至報表設計師，方法是在 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 中建立新的報表專案。 當您為報表建立新的資料集時，延伸模組應該會包含在可用資料來源類型的清單中。  
  
## <a name="see-also"></a>另請參閱  
 [部署資料處理延伸模組](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md)   
 [Reporting Services 延伸模組](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [實作資料處理延伸模組](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services 延伸模組程式庫](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  

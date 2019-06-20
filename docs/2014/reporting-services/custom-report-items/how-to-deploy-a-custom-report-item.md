---
title: HOW TO：部署自訂報表項目 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- custom report items, deploying
ms.assetid: 80e97b0d-e355-4240-aebd-08cbc84089ed
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2b41519ee6a6d31be33d92c8fbdf2ab503c93ec1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63265066"
---
# <a name="how-to-deploy-a-custom-report-item"></a>HOW TO：部署自訂報表項目
  若要在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中部署自訂報表項目，您必須修改報表伺服器組態檔，並將設計階段和執行階段元件組件複製到適當的報表設計師和報表伺服器應用程式資料夾中。  
  
### <a name="to-deploy-a-custom-report-item"></a>部署自訂報表項目  
  
1.  編輯 Rsreportdesigner.config 檔案，將自訂報表項目執行階段和設計階段元件設定為用於設計工具： 請注意，`ReportItemName` 項目必須符合用於 `CustomReportItemAttribute` 類別的 `CustomReportItemDesigner` 屬性。 例如：  
  
    ```  
    <ReportItems>  
       <ReportItem Name="Polygons" Type="PolygonsCRI.PolygonsCRI,PolygonsCRI"/>  
    </ReportItems>  
    <ReportItemDesigner>  
       <ReportItem Name="Polygons" Type="PolygonsCRI.PolygonsDesigner, PolygonsDesigner" />  
    </ReportItemDesigner>  
    <ReportItemConverter>  
       <Converter Source="Chart" Target="Polygons" Type="PolygonsCRI.PolygonsConverter, PolygonsDesigner" />  
    </ReportItemConverter>  
    ```  
  
2.  編輯 Rsreportserver.config 檔案來註冊自訂表單項目執行階段元件。 例如：  
  
    ```  
    <ReportItems>  
       <ReportItem Name="Polygons" Type="PolygonsCRI.PolygonsCRI,PolygonsCRI"/>  
    </ReportItems>  
    ```  
  
3.  編輯 Rsssrvpolicy.config 檔案以加入 `CodeGroup`，將適當的權限授與自訂報表項目。 例如：  
  
    ```  
    <CodeGroup   
       class="UnionCodeGroup"   
       version="1"   
       PermissionSetName="FullTrust"  
       Description="This code group grants MyCustomReportItem.dll FullTrust permission. ">  
       <IMembershipCondition   
          class="UrlMembershipCondition"  
          version="1"  
       Url="C:\Program Files\Microsoft SQL Server\ MSRS10_50.SQLSERVER\Reporting Services\ReportServer\bin\MyCustomReportItem.dll" />  
    </CodeGroup>  
    ```  
  
4.  將自訂報表項目執行階段元件 DLL 複製到 %ProgramFiles%\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies and \Program Files\Microsoft SQL Server\MSRS10_50.SQLSERVER\Reporting Services\ReportServer\bin 目錄。  
  
5.  將自訂報表項目設計階段元件 DLL 複製到 %ProgramFiles%\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies 目錄。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 組態檔](../report-server/reporting-services-configuration-files.md)   
 [自訂報表項目類別庫](custom-report-item-class-libraries.md)  
  
  

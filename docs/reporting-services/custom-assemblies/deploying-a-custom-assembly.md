---
title: 部署自訂組件 | Microsoft Docs
description: 了解如何在 SQL Server Reporting Services 中部署自訂組件。 另請了解如何將執行權限以外的權限授與自訂群組件。
ms.date: 11/23/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: custom-assemblies
ms.topic: reference
helpviewer_keywords:
- deploying custom assemblies [Reporting Services]
- custom assemblies [Reporting Services], deploying
- custom assemblies [Reporting Services], updating
- updating custom assemblies
ms.assetid: c6674cd8-0de7-4a5a-9e7c-12ffa49f6fd2
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 2c68562c1be1817d8f7457f680b4f45169de4a1f
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96166881"
---
# <a name="deploying-a-custom-assembly"></a>部署自訂組件
  若要在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中部署自訂組件，請在報表設計師與報表伺服器的應用程式資料夾中放置組件。 根據預設，會授與自訂組件在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中的 **Execution** 權限。 若要授與執行權限以外的自訂組件權限，您必須編輯報表伺服器的 rssrvpolicy.config 設定檔，以及報表設計師預覽視窗的 rspreviewpolicy.config 設定檔。 或者，您可以在全域組件快取 (GAC) 中安裝自訂組件。  
  
> [!NOTE]  
>  報表設計師有兩個預覽模式：當在 **DebugLocal** 模式中啟動報表專案時，會啟動 [預覽] 索引標籤與快顯預覽視窗。 [預覽] 索引標籤會使用 **FullTrust** 權限集合來執行所有的報表運算式，而且不會套用安全性原則設定。 快顯預覽視窗是用以模擬報表伺服器功能，因此具有原則組態檔，而且您或系統管理員必須修改該檔案，才能在報表設計師中使用自訂組件。 此快顯預覽也會鎖定自訂組件。 因此，您需要關閉預覽視窗，才能修改或是更新自訂組件程式碼。  
  
## <a name="to-deploy-a-custom-assembly-in-reporting-services"></a>在 Reporting Services 中部署自訂組件  
  
1.  將自訂組件從建立位置複製到報表伺服器 bin 資料夾或是報表設計師資料夾。 

     將自訂組件放在報表伺服器的 bin 資料夾中可讓您發行參考您自訂組件的報表。 報表伺服器之 bin 資料夾的預設位置是：

     Reporting Services 2016
     ```
     %ProgramFiles%\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\ReportServer\bin
     ```
     Reporting Services 2017 與更新版本
     ```
     %ProgramFiles%\Microsoft SQL Server Reporting Services\SSRS\ReportServer\bin
     ```
     將它放在報表設計師資料夾中可讓您在報表設計師中執行參考自訂組件的報表及針對那些報表進行偵錯。 報表設計師的預設位置是：

     Visual Studio 2012
     ```
     C:\Program Files (x86)\Microsoft Visual Studio 11.0\Common7\IDE\PrivateAssemblies
     ```
     Visual Studio 2013
     ```
     C:\Program Files (x86)\Microsoft Visual Studio 12.0\Common7\IDE\PrivateAssemblies
     ```
     Visual Studio 2015
     ```
     C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\PrivateAssemblies
     ```
     Visual Studio 2017
     ```
     C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\CommonExtensions\Microsoft\SSRS
     ```
     Visual Studio 2019
     ```
     C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\Common7\IDE\CommonExtensions\Microsoft\SSRS
     ```  
2.  開啟適當的組態檔。 報表伺服器之 rssrvpolicy.config 的預設位置是：

     Reporting Services 2016
     ```
     %ProgramFiles%\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\ReportServer
     ```
     Reporting Services 2017 與更新版本
     ```
     %ProgramFiles%\Microsoft SQL Server Reporting Services\SSRS\ReportServer
     ```
     要為報表設計師更新的檔案包括：

     Visual Studio 2012
     ```
     C:\Program Files (x86)\Microsoft Visual Studio 11.0\Common7\IDE\PrivateAssemblies\PreviewProcessingService.exe.config
     C:\Program Files (x86)\Microsoft Visual Studio 11.0\Common7\IDE\PrivateAssemblies\RSPreviewPolicy.config
     C:\Program Files (x86)\Microsoft Visual Studio 11.0\Common7\IDE\PrivateAssemblies\RSReportDesigner.config
     C:\Program Files (x86)\Microsoft Visual Studio 11.0\Common7\IDE\PrivateAssemblies\RSReportHost11.exe.config
     ```
     Visual Studio 2013
     ```
     C:\Program Files (x86)\Microsoft Visual Studio 12.0\Common7\IDE\PrivateAssemblies\PreviewProcessingService.exe.config
     C:\Program Files (x86)\Microsoft Visual Studio 12.0\Common7\IDE\PrivateAssemblies\RSPreviewPolicy.config
     C:\Program Files (x86)\Microsoft Visual Studio 12.0\Common7\IDE\PrivateAssemblies\RSReportDesigner.config
     C:\Program Files (x86)\Microsoft Visual Studio 12.0\Common7\IDE\PrivateAssemblies\RSReportHost.exe.config
     ```
     Visual Studio 2015
     ```
     C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\PrivateAssemblies\PreviewProcessingService.exe.config
     C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\PrivateAssemblies\RSPreviewPolicy.config
     C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\PrivateAssemblies\RSReportDesigner.config
     C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\PrivateAssemblies\RSReportHost.exe.config
     ```
     Visual Studio 2017
     ```
     C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\CommonExtensions\Microsoft\SSRS\PreviewProcessingService.exe.config
     C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\CommonExtensions\Microsoft\SSRS\RSPreviewPolicy.config
     C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\CommonExtensions\Microsoft\SSRS\RSReportDesigner.config
     C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\CommonExtensions\Microsoft\SSRS\RSReportHost.exe.config
     ```
     Visual Studio 2019
     ```
     C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\Common7\IDE\CommonExtensions\Microsoft\SSRS\PreviewProcessingService.exe.config
     C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\Common7\IDE\CommonExtensions\Microsoft\SSRS\RSPreviewPolicy.config
     C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\Common7\IDE\CommonExtensions\Microsoft\SSRS\RSReportDesigner.config
     C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\Common7\IDE\CommonExtensions\Microsoft\SSRS\RSReportHost.exe.config
     ```    
3.  為您的自訂組件加入程式碼群組。 如需詳細資訊，請參閱[安全開發 &#40;Reporting Services&#41;](../../reporting-services/extensions/secure-development/secure-development-reporting-services.md)。  
  
## <a name="updating-custom-assemblies"></a>更新自訂組件  
 在某些時候，您可能需要更新一些已發行報表目前已參考的自訂組件版本。 如果在報表伺服器或是報表設計師的 bin 目錄中已經有該組件，而且已遞增或是在某些方面已變更該組件的版本號碼，則目前發行的報表將無法再正常運作。 您將需要更新報表定義的 **CodeModules** 項目中所參考的組件版本，並重新發行報表。 如果您知道會經常更新自訂組件，而且目前發行的報表需要參考新組件，則可能會考慮在特定組件的所有更新之間使用相同的版本號碼。  
  
 如果您不需要目前發行的報表參考組件的新版本，可以將自訂組件部署到全域組件快取。 全域組件快取可以維護相同組件的多個版本，因此您目前的報表可以參考舊版的組件，而且新發行的報表可以參考更新的組件。 但是另一項方法將會設定報表伺服器的繫結重新導向，以強制將舊組件的所有要求重新導向至新組件。 您將需要修改報表伺服器 Web.config 檔案與報表伺服器 ReportingServicesService.exe.config 檔案。 項目可能如下所示：  
  
```  
<configuration>  
   <runtime>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
         <dependentAssembly>  
            <assemblyIdentity name="myAssembly"  
                              publicKeyToken="32ab4ba45e0a69a1"  
                              culture="neutral" />  
            <bindingRedirect oldVersion="1.0.0.0"  
                             newVersion="2.0.0.0"/>  
         </dependentAssembly>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>另請參閱  
 [將自訂組件與報表搭配使用](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)   
 [使用組件和全域組件快取](https://go.microsoft.com/fwlink/?LinkId=63912)  
  
  

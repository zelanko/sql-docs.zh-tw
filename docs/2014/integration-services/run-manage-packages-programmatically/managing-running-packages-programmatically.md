---
title: 以程式設計方式管理執行中的封裝 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- packages [Integration Services], managing
- running packages [Integration Services]
ms.assetid: 0e91f4ac-6f29-40d7-8c28-9b82e4802c35
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 42c4383692677c0e124e72b997fdca54707f4d03
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62889542"
---
# <a name="managing-running-packages-programmatically"></a>以程式設計方式管理執行中的封裝
  當您以程式設計方式處理 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝時，您可能會想要判斷目前正在執行的封裝。 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 命名空間的 <xref:Microsoft.SqlServer.Dts.Runtime> 類別提供了各種方法和類別來滿足這些需求。  
  
 如需監視封裝的詳細資訊，請參閱[封裝管理 &#40;SSIS 服務&#41;](../service/package-management-ssis-service.md)。  
  
 本主題中討論的所有方法都需要 `Microsoft.SqlServer.ManagedDTS` 組件的參考。 在新專案中加入參考之後，請使用 <xref:Microsoft.SqlServer.Dts.Runtime> 或 `using` 陳述式來匯入 `Imports` 命名空間。  
  
> [!IMPORTANT]  
>  用以搭配 SSIS 封裝存放區使用的 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 類別之方法，僅支援 "."、localhost 或是本機伺服器的伺服器名稱。 您無法使用 "(local)"。  
  
## <a name="determining-which-packages-are-currently-running"></a>判斷目前正在執行的封裝  
 若要判斷目前有哪些封裝正在指定的伺服器上執行，請呼叫 <xref:Microsoft.SqlServer.Dts.Runtime.Application.GetRunningPackages%2A> 方法。 這個方法會傳回 <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackages> 物件的 <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage> 集合。  
  
> [!NOTE]  
>  管理員會看到目前正在電腦上執行的所有封裝；其他使用者只能看到已經啟動的封裝。  
  
## <a name="working-with-running-packages"></a>處理執行中的封裝  
 當您判斷哪些封裝目前正在執行之後，您可以擷取有關封裝的資訊，並要求封裝停止。  
  
### <a name="getting-information-about-a-running-package"></a>取得有關執行中封裝的資訊  
 當您反覆運算 <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackages> 集合時，您可以使用 <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage> 物件的屬性，以尋找封裝或取得有關正在執行之封裝的其他資訊：  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.ExecutionDuration%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.ExecutionStartTime%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.InstanceID%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.PackageDescription%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.PackageID%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.PackageName%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.UserName%2A>  
  
### <a name="stopping-a-running-package"></a>停止執行中的封裝  
 您可以呼叫 <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.Stop%2A> 物件的 <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage> 方法，要求此封裝停止。 在發出停止要求的時間與封裝實際停止的時間之間可能會有延遲。  
  
![Integration Services 圖示（小型）](../media/dts-16.gif "Integration Services 圖示 (小)")**與 Integration Services 保持最**新狀態  <br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。  
  
## <a name="see-also"></a>另請參閱  
 [套件管理 &#40;SSIS 服務&#41;](../service/package-management-ssis-service.md)   
 [以程式設計方式列舉可用的套件](../run-manage-packages-programmatically/enumerating-available-packages-programmatically.md)  
  
  

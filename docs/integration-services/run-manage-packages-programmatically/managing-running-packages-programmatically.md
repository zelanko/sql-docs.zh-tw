---
title: "管理以程式設計方式執行封裝 |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: run-manage-packages-programmatically
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- packages [Integration Services], managing
- running packages [Integration Services]
ms.assetid: 0e91f4ac-6f29-40d7-8c28-9b82e4802c35
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: 34f2c773e89c0162df5d13a16d27f01eb5d8f4df
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="managing-running-packages-programmatically"></a>以程式設計方式管理執行中的封裝
  當您以程式設計方式處理 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝時，您可能會想要判斷目前正在執行的封裝。 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 命名空間的 <xref:Microsoft.SqlServer.Dts.Runtime> 類別提供了各種方法和類別來滿足這些需求。  
  
 如需有關如何監視封裝的詳細資訊，請參閱[封裝管理 &#40;SSIS 服務 &#41;](../../integration-services/service/package-management-ssis-service.md).  
  
 本主題所討論的所有方法都必須參考**Microsoft.SqlServer.ManagedDTS**組件。 在新的專案中加入參考之後，匯入<xref:Microsoft.SqlServer.Dts.Runtime>命名空間與**使用**或**匯入**陳述式。  
  
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
  
## <a name="see-also"></a>另請參閱  
 [封裝管理 &#40;SSIS 服務 &#41;](../../integration-services/service/package-management-ssis-service.md)   
 [以程式設計方式列舉可用的封裝](../../integration-services/run-manage-packages-programmatically/enumerating-available-packages-programmatically.md)  
  
  


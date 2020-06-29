---
title: 開發自訂工作 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom tasks [Integration Services], about custom tasks
- Task class
- custom tasks [Integration Services]
- SSIS custom tasks
- SSIS custom tasks, about custom tasks
- IDtsTaskUI interface
- DtsTaskAttribute attribute
- tasks [Integration Services], custom
- TaskHost object
ms.assetid: dcbd8615-fa6d-4ddb-b8a5-0b19dddd6239
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b4257d883b1f39e918f0f8a6eb8135e25b784a79
ms.sourcegitcommit: 04ba0ed3d860db038078609d6e348b0650739f55
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/27/2020
ms.locfileid: "85469283"
---
# <a name="developing-a-custom-task"></a>開發自訂工作
  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 利用工作執行工作單位，以支援擷取、轉換及載入資料。 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 包含各種可以執行最常使用之動作的工作，包括執行 SQL 陳述式、從 FTP 站台下載檔案等。 如果包含的工作與支援的動作未完全符合您的需求，可以建立自訂工作。  
  
 若要建立自訂工作，您必須建立繼承[自的類別](/dotnet/api/microsoft.sqlserver.dts.runtime.task)、將 <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute> 屬性套用至您的新類別，並覆寫基類的重要方法和屬性，包括 <xref:Microsoft.SqlServer.Dts.Runtime.Task.Execute%2A> 方法在內。  
  
## <a name="in-this-section"></a>本節內容  
 本章節描述如何建立和設定自訂工作及其選用自訂使用者介面，以及如何撰寫它們的程式碼。  
  
 [建立自訂工作](creating-a-custom-task.md)  
 描述第一個步驟：建立自訂工作。  
  
 [撰寫自訂工作的程式碼](coding-a-custom-task.md)  
 描述如何撰寫自訂工作之主要方法的程式碼。  
  
 [在自訂工作中連線至資料來源](connecting-to-data-sources-in-a-custom-task.md)  
 描述如何將自訂工作連接到資料來源。  
  
 [在自訂工作中引發和定義事件](raising-and-defining-events-in-a-custom-task.md)  
 描述如何引發事件並從自訂工作定義自訂事件。  
  
 [在自訂工作中為偵錯新增支援](adding-support-for-debugging-in-a-custom-task.md)  
 描述如何在自訂工作中建立中斷點目標。  
  
 [開發自訂工作的使用者介面](developing-a-user-interface-for-a-custom-task.md)  
 描述如何建立顯示在 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師中的使用者介面，以便在自訂工作上設定屬性。  
  
## <a name="related-sections"></a>相關章節  
  
### <a name="information-common-to-all-custom-objects"></a>自訂物件的共通資訊  
 如需有關 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 中可以建立之所有類型自訂物件適用的共通資訊，請參閱下列主題：  
  
 [開發 Integration Services 的自訂物件](../developing-custom-objects-for-integration-services.md)  
 描述為 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 實作所有種類的自訂物件之基本步驟。  
  
 [保存自訂物件](../persisting-custom-objects.md)  
 描述自訂的持續性並解釋必須實作它的時機。  
  
 [自訂物件的建立、部署和偵錯](../building-deploying-and-debugging-custom-objects.md)  
 描述建立、簽署、部署和偵錯自訂物件的技術。  
  
### <a name="information-about-other-custom-objects"></a>其他自訂物件的相關資訊  
 如需有關在 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 中可以建立之其他類型自訂物件的詳細資訊，請參閱下列主題：  
  
 [開發自訂連線管理員](../connection-manager/developing-a-custom-connection-manager.md)  
 討論如何進行自訂連接管理員的程式設計。  
  
 [開發自訂記錄提供者](../log-provider/developing-a-custom-log-provider.md)  
 討論如何進行自訂記錄提供者的程式設計。  
  
 [開發自訂 Foreach 列舉程式](../foreach-enumerator/developing-a-custom-foreach-enumerator.md)  
 討論如何進行自訂列舉值的程式設計。  
  
 [開發自訂資料流程元件](../data-flow/developing-a-custom-data-flow-component.md)  
 討論如何進行自訂資料流程來源、轉換和目的地的程式設計。  
  
![Integration Services 圖示（小型）](../../media/dts-16.gif "Integration Services 圖示 (小)")**與 Integration Services 保持最**新狀態  <br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。  
  
## <a name="see-also"></a>另請參閱  
 [使用腳本工作擴充封裝](../../extending-packages-scripting/task/extending-the-package-with-the-script-task.md)   
 [比較指令碼方案和自訂物件](../../extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)  
  
  

---
title: "使用自訂物件擴充封裝 |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 26616eb8-9e80-434d-b22a-ece1b00f449d
caps.latest.revision: 36
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e10fbab75eca8556e36734c1c0ad3828b8b09404
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="extending-packages-with-custom-objects"></a>使用自訂物件擴充封裝
  如果發現 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中提供的元件不符合需求，可以編寫自己的延伸模組，擴充 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的功能。 您有兩個完全不同的選項可擴充封裝：其一是在指令碼工作與指令碼元件所提供的強大包裝函數中撰寫程式碼；其二則是可以從 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 物件模型提供的基底類別衍生，從頭建立自訂 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 延伸模組。  
  
 本章節探索兩個選項當中更進階的部分：以自訂物件擴充封裝。  
  
 您的自訂 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 方案需要的彈性比指令碼工作和指令碼元件所提供的彈性還要大，或您需要可在多個封裝中重複使用的元件時，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 物件模型可讓您從頭建立自訂工作、資料流程元件和 Managed 程式碼中的其他封裝物件。  
  
## <a name="in-this-section"></a>本節內容  
 [開發 Integration Services 的自訂物件](../../integration-services/extending-packages-custom-objects/developing-custom-objects-for-integration-services.md)  
 討論可以針對 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 建立的自訂物件以及摘要列出重要的步驟和設定。  
  
 [保存自訂物件](../../integration-services/extending-packages-custom-objects/persisting-custom-objects.md)  
 討論自訂物件的預設持續性及實作自訂持續性的程序。  
  
 [自訂物件的建立、部署和偵錯](../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)  
 討論建立、部署及測試各種類型之自訂物件的常用方法。  
  
 [開發自訂工作](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)  
 描述編寫自訂工作的程序。  
  
 [開發自訂連接管理員](../../integration-services/extending-packages-custom-objects/connection-manager/developing-a-custom-connection-manager.md)  
 描述編寫自訂連接管理員的程序。  
  
 [開發自訂記錄提供者](../../integration-services/extending-packages-custom-objects/log-provider/developing-a-custom-log-provider.md)  
 描述編寫自訂記錄提供者的程序。  
  
 [開發自訂 ForEach 列舉值](../../integration-services/extending-packages-custom-objects/foreach-enumerator/developing-a-custom-foreach-enumerator.md)  
 描述編寫自訂列舉值的程序。  
  
 [開發自訂資料流程元件](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)  
 討論如何進行自訂資料流程來源、轉換和目的地的程式設計。  
  
## <a name="reference"></a>참조  
 [Integration Services 錯誤和訊息參考](../../integration-services/integration-services-error-and-message-reference.md)  
 列出預先定義的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 錯誤碼，以及其符號名稱與描述。  
  
## <a name="related-sections"></a>相關章節  
 [使用指令碼擴充封裝](../../integration-services/extending-packages-scripting/extending-packages-with-scripting.md)  
 討論如何使用指令碼工作來擴充控制流程，或是如何使用指令碼元件來擴充資料流程。  
  
 [以程式設計方式建立封裝](../../integration-services/building-packages-programmatically/building-packages-programmatically.md)  
 描述如何以程式設計方式建立、設定、執行、載入、儲存和管理 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝。  
  
## <a name="see-also"></a>另請參閱  
 [比較指令碼方案和自訂物件](../../integration-services/extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)   
 [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)  
  
  


---
title: 稽核轉換 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.audittrans.f1
- sql13.dts.designer.audittransformation.f1
helpviewer_keywords:
- environment data in packages [Integration Services]
- Audit transformation
ms.assetid: 8c143682-9c81-4150-83d6-1d9678151d37
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9161fe71f82d2ca0f2f31805dc07beba387bc28d
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/16/2019
ms.locfileid: "65726296"
---
# <a name="audit-transformation"></a>稽核轉換

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  稽核轉換可讓封裝中的資料流程包含有關封裝執行的環境資料。 例如，可以將封裝、電腦與操作員的名稱加入資料流程。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 包括提供此資訊的系統變數。  
  
## <a name="system-variables"></a>系統變數  
 下表描述「稽核」轉換可使用的系統變數。  
  
|系統變數|索引|Description|  
|---------------------|-----------|-----------------|  
|**ExecutionInstanceGUID**|0|識別封裝執行執行個體的 GUID。|  
|**PackageID**|1|封裝的唯一識別碼。|  
|**PackageName**|2|封裝名稱。|  
|**VersionID**|3|封裝的版本。|  
|**ExecutionStartTime**|4|封裝開始執行的時間。|  
|**MachineName**|5|電腦名稱。|  
|**UserName**|6|啟動封裝之人員的登入名稱。|  
|**TaskName**|7|與「稽核」轉換相關聯的「資料流程」工作名稱。|  
|**TaskId**|8|「資料流程」工作的唯一識別碼。|  
  
## <a name="configuration-of-the-audit-transformation"></a>設定稽核轉換  
 您可藉由提供要加入至轉換輸出的新輸出資料行名稱來設定「稽核」轉換，然後將系統變數對應到輸出資料行。 您可以將單一系統變數對應到多個資料行。  
  
 此轉換有一個輸入和一個輸出。 它不支援錯誤輸出。  
  
 您可以透過 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 **[進階編輯器]** 對話方塊會反映能以程式設計的方式設定之屬性。 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [通用屬性](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [轉換自訂屬性](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 如需如何設定屬性的詳細資訊，請參閱 [設定資料流程元件的屬性](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="audit-transformation-editor"></a>稽核轉換編輯器
  稽核轉換可讓封裝中的資料流程包含有關封裝執行的環境資料。 例如，可以將封裝、電腦與操作員的名稱加入資料流程。 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 包括提供此資訊的系統變數。  
  
### <a name="options"></a>選項。  
 **輸出資料行名稱**  
 提供包含稽核資訊之新輸出資料行的名稱。  
  
 **稽核類型**  
 選取可用的系統變數以提供稽核資訊。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**執行執行個體 GUID**|插入唯一識別封裝之執行執行個體的 GUID。|  
|**封裝識別碼**|插入唯一識別封裝的 GUID。|  
|**封裝名稱**|插入封裝名稱。|  
|**版本識別碼**|插入唯一識別封裝版本的 GUID。|  
|**執行開始時間**|插入封裝開始執行的時間。|  
|**電腦名稱**|插入啟動封裝的電腦名稱。|  
|**User name**|插入啟動封裝之使用者的登入名稱。|  
|**工作名稱**|插入與稽核轉換相關聯之資料流程工作的名稱。|  
|**工作識別碼**|插入唯一識別與稽核轉換相關聯之資料流程工作的 GUID。|  
  
  

---
title: 稽核轉換 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.audittrans.f1
helpviewer_keywords:
- environment data in packages [Integration Services]
- Audit transformation
ms.assetid: 8c143682-9c81-4150-83d6-1d9678151d37
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b667df1872aa4765f9c82ebaa6e83b2fa1cf480c
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85431175"
---
# <a name="audit-transformation"></a>稽核轉換
  稽核轉換可讓封裝中的資料流程包含有關封裝執行的環境資料。 例如，可以將封裝、電腦與操作員的名稱加入資料流程。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 包含提供此資訊的系統變數。  
  
## <a name="system-variables"></a>系統變數  
 下表描述「稽核」轉換可使用的系統變數。  
  
|系統變數|索引|描述|  
|---------------------|-----------|-----------------|  
|`ExecutionInstanceGUID`|0|識別封裝執行執行個體的 GUID。|  
|`PackageID`|1|封裝的唯一識別碼。|  
|`PackageName`|2|封裝名稱。|  
|`VersionID`|3|封裝的版本。|  
|`ExecutionStartTime`|4|封裝開始執行的時間。|  
|`MachineName`|5|電腦名稱。|  
|`UserName`|6|啟動封裝之人員的登入名稱。|  
|`TaskName`|7|與「稽核」轉換相關聯的「資料流程」工作名稱。|  
|**TaskId**|8|「資料流程」工作的唯一識別碼。|  
  
## <a name="configuration-of-the-audit-transformation"></a>設定稽核轉換  
 您可藉由提供要加入至轉換輸出的新輸出資料行名稱來設定「稽核」轉換，然後將系統變數對應到輸出資料行。 您可以將單一系統變數對應到多個資料行。  
  
 此轉換有一個輸入和一個輸出。 它不支援錯誤輸出。  
  
 您可以透過 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需可在 **[稽核轉換編輯器]** 對話方塊中設定之屬性的詳細資訊，請參閱 [Audit Transformation Editor](../../audit-transformation-editor.md)。  
  
 **[進階編輯器]** 對話方塊會反映能以程式設計的方式設定之屬性。 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [Common Properties](../../common-properties.md)  
  
-   [轉換自訂屬性](transformation-custom-properties.md)  
  
 如需如何設定屬性的詳細資訊，請參閱 [設定資料流程元件的屬性](../set-the-properties-of-a-data-flow-component.md)。  
  
  

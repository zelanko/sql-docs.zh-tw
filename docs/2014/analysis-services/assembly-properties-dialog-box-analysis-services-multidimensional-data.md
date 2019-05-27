---
title: 組件屬性對話方塊 (Analysis Services-多維度資料) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.assemblyproperties.f1
ms.assetid: da1174d6-d82b-4337-ac19-7368dbd95a84
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b21230ddff5a3db043b533a4f921a30b02da739b
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66062300"
---
# <a name="assembly-properties-dialog-box-analysis-services---multidimensional-data"></a>組件屬性對話方塊 (Analysis Services - 多維度資料)
  使用 **中的** [組件屬性] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 對話方塊，即可設定 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫中之組件參考的屬性。 以滑鼠右鍵按一下物件總管中的組件，然後選取 [屬性]，即可顯示 [組件屬性] 對話方塊。  
  
## <a name="options"></a>選項  
  
|詞彙|定義|  
|----------|----------------|  
|**名稱**|鍵入即可變更組件參考的名稱。<br /><br /> 注意:變更此值不會變更組件參考所參考的組件名稱，但會變更 使用的名稱所[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]執行個體或資料庫在參考組件參考時。|  
|**ID**|顯示組件參考所參考的組件識別碼。|  
|**說明**|鍵入即可變更組件參考的描述。|  
|**建立時間戳記**|顯示建立組件參考的日期和時間。|  
|**上次結構描述更新**|顯示上次更新組件參考之中繼資料的日期和時間。|  
|**型別**|顯示組件參考的類型。 會顯示下列各值：<br /><br /> **.NET 組件**：組件參考所參考的是 [!INCLUDE[msCoName](../includes/msconame-md.md)] .NET Framework 組件。<br /><br /> **COM DLL**：組件參考所參考的是 COM 程式庫。|  
|**Source**|顯示組件參考的來源。 這個屬性通常包含組件參考所參考之組件的完整路徑和檔案名稱。|  
|**權限集合**|選取用來決定是否可以存取組件參考的權限集合。 如需有關此屬性之可用值的詳細資訊，請參閱 <xref:Microsoft.AnalysisServices.ClrAssembly.PermissionSet%2A>。|  
|**模擬資訊**|選取在存取組件參考時要使用的模擬資訊。 如需此屬性之可用值的詳細資訊，請參閱 [ImpersonationInfo 元素 &#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/properties/impersonationinfo-element-assl)|  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services Designers and Dialog Boxes&#40;多維度資料&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [多維度模型組件管理](multidimensional-models/multidimensional-model-assemblies-management.md)  
  
  

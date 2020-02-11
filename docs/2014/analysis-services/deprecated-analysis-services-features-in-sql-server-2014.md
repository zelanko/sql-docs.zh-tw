---
title: SQL Server 2014 中已淘汰的 Analysis Services 功能 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services, backward compatibility
- SSAS, backward compatibility
- SQL Server Analysis Services, backward compatibility
- deprecated features [Analysis Services]
ms.assetid: 2c96ecfe-a170-41d0-bee3-74503f880197
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 04d12aab677e38d17d4e869e6885eb470854d824
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66081914"
---
# <a name="deprecated-analysis-services-features-in-sql-server-2014"></a>SQL Server 2014 中已被取代的 Analysis Services 功能
  本主題描述 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中仍然可用但已被取代的 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]功能。 這些功能將在未來的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]版本中移除。 已被取代的功能不應在新應用程式中使用。  
  
## <a name="features-not-supported-in-the-next-version-of-sql-server"></a>下一版的 SQL Server 不支援的功能  
 下一版的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 將不再支援以下 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]功能。 請勿在新的開發工作中使用這些功能，並且儘速修改使用這些功能的應用程式。  
  
|類別|已被取代的功能|取代|  
|--------------|------------------------|-----------------|  
|MDX 函數|CalculationPassValue 函數|無。 OLAP 引擎會管理計算行程。 不再需要這個函數。|  
|MDX 函數|CalculationCurrentPass 函數|無。 OLAP 引擎會管理計算行程。 不再需要這個函數。|  
|多維度運算式 (MDX)|NON_EMPTY_BEHAVIOR 查詢最佳化工具提示預設為啟動。|NON_EMPTY_BEHAVIOR 查詢最佳化工具提示在未來版本中會預設為關閉。 這是 MDX 最佳化提示，如果沒有正確地使用，可能會產生不正確的結果。|  
|其他|CELL_EVALUATION_LIST 內建資料格屬性|原本提供套用至資料格之評估公式的清單。 這個清單在此版 Analysis Services 中是空白的。  求解順序現在是以 MDX 指令碼指定。 如需詳細資訊，請參閱[瞭解行程順序和解決順序 &#40;MDX&#41;](multidimensional-models/mdx/mdx-data-manipulation-understanding-pass-order-and-solve-order.md)|  
|物件|COM 組件|COM 組件可能會造成安全性風險。 未來的版本將移除 COM 組件的支援。|  
  
## <a name="features-not-supported-in-a-future-version-of-sql-server"></a>SQL Server 的未來版本不支援的功能  
 下一版的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 可支援下列 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]功能，但會在更新的版本中移除。 確實的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本尚未決定。  
  
|類別|已被取代的功能|取代|  
|--------------|------------------------|-----------------|  
|多維度模型|遠端分割區|無。 請改用本機分割區。 如需詳細資訊，請參閱[建立和管理本機資料分割 &#40;Analysis Services&#41;](multidimensional-models/create-and-manage-a-local-partition-analysis-services.md) 。|  
|多維度模型|遠端連結量值群組|遠端連結量值群組是使用遠端伺服器上資料來源的連結量值群組。 現已排定要取代連結量值群組可使用遠端資料來源這項功能。<br /><br /> 此功能尚無替代項目。 建議您改用本機連結量值群組。 如需相關資訊，請參閱 [Linked Measure Groups](multidimensional-models/linked-measure-groups.md) 。|  
|多維度模型|維度回寫|無。 如果您需要回寫功能，請使用分割區回寫。 如需詳細資訊，請參閱[設定分割區回寫](multidimensional-models/set-partition-writeback.md)。|  
|多維度模型|連結維度|無。 請考慮將維度複製到其他模型，而不要連結到位於另一個模型的維度。|  
|MDX|Non_Empty_Behavior 屬性|無。 建立導出成員時若此屬性的設定不正確，可能會增加傳回不正確結果的機率。 在 OLAP 引擎最近的最佳化中，已改善對疏鬆資料集的作業，降低此屬性的相關性。|  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 回溯相容性](analysis-services-backward-compatibility.md)   
 [SQL Server 2014 中已停止的 Analysis Services 功能](discontinued-analysis-services-functionality-in-sql-server-2014.md)  
  
  

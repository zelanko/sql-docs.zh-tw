---
title: 使用分析管理物件 (AMO) 來開發 |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: amo
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f63a866bc2ee61eeb7ec7aecff680540f039f7a8
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="developing-with-analysis-management-objects-amo"></a>使用分析管理物件 (AMO) 來開發
分析管理物件 (AMO) 是以程式設計方式存取物件的可讓應用程式管理的執行個體的完整程式庫[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。

本章節說明的 AMO 概念著重在主要物件，並且會包括使用的方式與時機，以及這些物件互相關聯的方式。 如需有關特定物件或類別的詳細資訊，請參閱：

- [Microsoft.AnalysisServices 命名空間](http://msdn.microsoft.com/library/microsoft.analysisservices.aspx)，如參考文件
- [Analysis Services 管理物件 (AMO)](http://www.bing.com/search?q=Analysis+Services+Management+Objects+%28AMO%29)，做為 Bing.com 一般搜尋。


 **SQL Server 2016 的新功能**

在 SQL Server 2016 中，AMO 已重構為多個組件。 泛型類別，例如伺服器、 資料庫和角色正在**Microsoft.AnalysisServices.Core**命名空間。 多維度專屬的 Api 會保留在[Microsoft.AnalysisServices 命名空間](https://msdn.microsoft.com/library/ms146720.aspx)。

自訂指令碼以及針對較早版本的 AMO 所撰寫的應用程式將繼續運作並進行任何修改。 不過，如果您有指令碼或應用程式目標的 SQL Server 2016 具體來說，或是您需要重新建置自訂解決方案，務必將新的組件和命名空間加入至專案。

## <a name="see-also"></a>另請參閱
[使用 Analysis Services 開發的指令碼語言&#40;ASSL&#41;](../../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)
[使用 Analysis Services 中的 XMLA 進行開發](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)

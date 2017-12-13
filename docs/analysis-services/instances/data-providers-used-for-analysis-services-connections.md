---
title: "用於 Analysis Services 連接的資料提供者 |Microsoft 文件"
ms.custom: 
ms.date: 12/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 128f6dde-409d-4c12-9820-3305bab57b75
caps.latest.revision: "19"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 10f2596b6a2111fac89fc996bf6be521d7158f5d
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="client-libraries-data-providers-used-for-analysis-services-connections"></a>使用 Analysis services 連接的用戶端程式庫 （資料提供者）
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]

Analysis Services 提供三個用戶端程式庫，也稱為**資料提供者**、 伺服器和資料存取工具和用戶端應用程式。 工具，例如 SSMS 和 SSDT 中，以及應用程式像是 Power BI Desktop 和 Excel 連接到 Analysis Services 使用這些程式庫。 ADOMD.NET 和 Analysis Services 管理物件 (AMO)，用戶端程式庫是受管理的用戶端程式庫。 Analysis Services OLE DB 提供者 (MSOLAP DLL) 是原生用戶端程式庫。 
  
##  <a name="bkmk_downloadsite"></a>何處可取得較新版本  
 用戶端電腦上安裝的版本應與提供資料的伺服器主要版本相符。 如果伺服器安裝比網路中工作站上安裝的資料提供者還要新，您可能需要安裝較新版的程式庫。  

包含在舊版的 SQL Server Feature Pack 的用戶端程式庫對應至該 SQL 版本。不過，它們可能不是最新。 連接到 Azure Analysis Services 可能需要更新的版本。 所有版本都都具有回溯相容性。

若要取得最新，請參閱[用戶端程式庫連接到 Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-data-providers)。 
  
## <a name="see-also"></a>另請參閱  
 [連接到 Analysis Services](../../analysis-services/instances/connect-to-analysis-services.md)  
  
  

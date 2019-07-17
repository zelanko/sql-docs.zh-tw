---
title: Analysis Services 的鎖定管理員屬性 |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a5383fe83963a9b388413b9b829b4fac7fc11788
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "68207969"
---
# <a name="lock-manager-properties"></a>鎖定管理員屬性
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支援下表列出的鎖定管理員伺服器屬性。 如需其他伺服器屬性以及如何設定伺服器屬性的詳細資訊，請參閱 [Analysis Services 中的伺服器屬性](../../analysis-services/server-properties/server-properties-in-analysis-services.md)。  
  
 **適用於：** 多維度與表格式伺服器模式  
  
## <a name="properties"></a>屬性  
 **DefaultLockTimeoutMS**  
 此為帶正負號的 32 位元整數屬性，定義內部鎖定要求的預設鎖定逾時 (以毫秒為單位)。  
  
 此屬性的預設值為 -1，指出內部鎖定要求沒有逾時。  
  
 **LockWaitGranularityMS**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 **DeadlockDetectionGranularityMS**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 中的伺服器屬性](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [判斷 Analysis Services 執行個體的伺服器模式](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  

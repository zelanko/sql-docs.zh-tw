---
title: 鎖定管理員屬性 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- lock manager properties [Analysis Services]
- LockWaitGranularityMS property
- DefaultLockTimeoutMS property
- DeadlockDetectionGranularityMS property
ms.assetid: 15fe9ead-825b-4ac3-9191-7a07caa2861b
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 39b1c209bb8993483628af89ac7e80b558862436
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36034226"
---
# <a name="lock-manager-properties"></a>鎖定管理員屬性
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支援下表列出的鎖定管理員伺服器屬性。 如需有關其他伺服器屬性及如何設定伺服器屬性的詳細資訊，請參閱＜ [Configure Server Properties in Analysis Services](server-properties-in-analysis-services.md)＞。  
  
 **適用於：** 多維度與表格式伺服器模式  
  
## <a name="properties"></a>屬性  
 `DefaultLockTimeoutMS`  
 此為帶正負號的 32 位元整數屬性，定義內部鎖定要求的預設鎖定逾時 (以毫秒為單位)。  
  
 此屬性的預設值為 -1，指出內部鎖定要求沒有逾時。  
  
 `LockWaitGranularityMS`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `DeadlockDetectionGranularityMS`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 中設定伺服器屬性](server-properties-in-analysis-services.md)   
 [判斷 Analysis Services 執行個體的伺服器模式](../instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
---
title: 在報表伺服器電腦上偵測到過時的延伸模組（Upgrade Advisor） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], upgrade issues
ms.assetid: 40d245a2-0631-470e-81b3-1feb47e028cb
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 18f90bd6c551a6240a49eed9a0ec39723851bce1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "71952072"
---
# <a name="obsolete-extensions-were-detected-on-the-report-server-computer-upgrade-advisor"></a>在報表伺服器電腦上偵測到過時的延伸模組 (Upgrade Advisor)
  Upgrade Advisor 偵測到一個或多個在目前版本中已經無法使用的轉譯延伸模組。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式 &#124; [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式。|  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>描述  
 報表伺服器設定為使用一或多個在這個版本中已經停止的延伸模組。 已停止的延伸模組包括：  
  
-   HTML OWC 轉譯延伸模組  
  
-   HTML 3.2 轉譯延伸模組  
  
 雖然升級可以繼續進行，但是不支援的功能將無法在升級的報表伺服器上使用。  
  
 如果您需要使用這些延伸模組，在找到這些需求的替代方案之前，請勿進行升級。 您可能必須取得或建立可提供相同或類似功能的自訂轉譯延伸模組。  
  
## <a name="corrective-action"></a>更正動作  
 評估目前 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中所包含的功能集，以便判斷支援的功能是否符合您的需求。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Upgrade Advisor Reporting Services 升級問題&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  

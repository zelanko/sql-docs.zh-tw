---
title: IP 位址限制偵測到 (Upgrade Advisor) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], upgrade issues
ms.assetid: 9a154455-c68f-4403-a3a7-b90f4d35eecb
caps.latest.revision: 10
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 9dd20d23fbb18f67116d021b725796418ea2ccca
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37323748"
---
# <a name="ip-address-restriction-detected-upgrade-advisor"></a>偵測到 IP 位址限制 (Upgrade Advisor)
  Upgrade Advisor 在主控報表伺服器或報表管理員虛擬目錄的 IIS 網站上偵測到一個或多個 IP 位址限制。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 不會提供 IP 位址限制的原生支援。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生。|  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>描述  
 安裝程式無法針對升級報表伺服器所建立的 URL 定義 IP 位址限制。 雖然升級可以繼續進行，但是不會針對 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] URL 定義 IP 位址限制。  
  
## <a name="corrective-action"></a>更正動作  
 升級之後，請使用 ISA Server、防火牆軟體或其他解決方案來允許或排除特定 IP 位址到報表伺服器的要求。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 升級問題&#40;Upgrade Advisor&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  

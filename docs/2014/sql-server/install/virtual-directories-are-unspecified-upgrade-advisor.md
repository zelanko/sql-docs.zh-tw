---
title: 未指定虛擬目錄 (Upgrade Advisor) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- virtual directories [Reporting Services]
ms.assetid: 7d32b560-49d6-4558-b5d6-9127067f82d6
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: f5e0643fad0a9e554c3c89f1d1c546a7ab69534d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66091070"
---
# <a name="virtual-directories-are-unspecified-upgrade-advisor"></a>未指定虛擬目錄 (Upgrade Advisor)
  Upgrade Advisor 未偵測到報表伺服器 Web 服務或報表管理員的虛擬目錄設定。 升級完成之後，您必須使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員來設定報表伺服器的 URL 保留項目。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式|  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>描述  
 升級 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝包括保留報表伺服器 Web 服務和報表管理員的新 URL。 Upgrade Advisor 未偵測到要升級之執行個體的報表伺服器或報表管理員的虛擬目錄，因此升級程序的資訊不足，無法建立升級報表伺服器的 URL 保留項目。 雖然升級可以繼續進行，但是在升級的安裝之後，報表伺服器或報表管理員虛擬目錄將處於未定義狀態。  
  
## <a name="corrective-action"></a>更正動作  
 升級完成之後，請使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員來設定報表伺服器和報表管理員的 URL。 您可以使用 IIS 管理員來移除任何不再需要的虛擬目錄。  
  
 如需詳細資訊，請參閱 <<c0> [ 設定 URL &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]線上叢書 》。</c0>  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 升級問題&#40;Upgrade Advisor&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  

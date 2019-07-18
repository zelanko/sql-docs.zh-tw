---
title: 虛擬目錄中有不支援的驗證方法 (Upgrade Advisor) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- virtual directories [Reporting Services]
ms.assetid: 216eca6f-9a66-42e1-aa54-dcf99cec9f7d
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 992e0f125d80a4735a356a853dab55439149e7ba
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66091059"
---
# <a name="virtual-directory-has-unsupported-authentication-method-upgrade-advisor"></a>虛擬目錄具有不支援的驗證方法 (Upgrade Advisor)
  Upgrade Advisor 在報表管理員或報表伺服器虛擬目錄上偵測到不支援的驗證方法。 升級不支援的驗證方法包括匿名驗證、摘要式驗證和 .NET Passport。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式|  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>描述  
 安裝程式無法升級使用下列其中一種驗證方法的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝  
  
-   匿名  
  
-   Digest  
  
-   .NET Passport  
  
 若要繼續進行，您可以修改 Internet Information Services (IIS) 中針對 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 虛擬目錄指定的驗證方法，也可以移轉安裝。 如需有關移轉安裝的詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》。  
  
## <a name="corrective-action"></a>更正動作  
 若要繼續進行升級，請在 IIS 中針對 ReportServer 和 Reports 虛擬目錄修改驗證方法。 如需有關在 IIS 中修改驗證方法的詳細資訊，請參閱 IIS 文件集。 在您針對 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 虛擬目錄修改驗證方法之後，請重新執行 Upgrade Advisor 來確認沒有其他升級問題。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 升級問題&#40;Upgrade Advisor&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  

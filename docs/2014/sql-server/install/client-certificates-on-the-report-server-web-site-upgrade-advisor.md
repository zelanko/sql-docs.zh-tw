---
title: 報表伺服器網站上的用戶端憑證（Upgrade Advisor） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], upgrade issues
ms.assetid: 5ecce26b-99df-4109-8e51-d150d369dff7
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 5588930efbadf785e78aa115ad0021bce64bd7f7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "71952606"
---
# <a name="client-certificates-on-the-report-server-web-site-upgrade-advisor"></a>報表伺服器網站上的用戶端憑證 (Upgrade Advisor)
  Upgrade Advisor 在主控報表伺服器或報表管理員虛擬目錄的 IIS 網站上偵測到一或多個用戶端憑證。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]原生模式。|  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>描述  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]不支援使用用戶端憑證來驗證使用者。 雖然升級可以繼續進行，但是升級的報表伺服器將不會使用用戶端憑證。  
  
## <a name="corrective-action"></a>更正動作  
 您必須使用個別的解決方案 (例如 ISA Server) 來確保任何用戶端憑證驗證需求都會獲得處理。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Upgrade Advisor Reporting Services 升級問題&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  

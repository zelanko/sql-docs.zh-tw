---
title: 不是報表伺服器資料庫設定 (Upgrade Advisor) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- report servers [Reporting Services], upgrade issues
ms.assetid: b964300c-b220-4244-9fa6-c0c6a57760f6
caps.latest.revision: 14
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: f86e9963750d2bacbdc55e235e4975a05c2f625e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36037378"
---
# <a name="report-server-database-is-not-configured-upgrade-advisor"></a>未設定報表伺服器資料庫 (Upgrade Advisor)
  由於報表伺服器組態不完整，因此系統封鎖了升級。 未設定報表伺服器資料庫。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式 &#124; [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式。|  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>描述  
 安裝程式只能升級已完全設定的報表伺服器執行個體。 若要繼續，您必須設定報表伺服器資料庫，或使用 Microsoft Windows**控制台**移除報表伺服器功能從[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安裝。 在您移除 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 之後，就可以升級其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件。  
  
## <a name="corrective-action"></a>更正動作  
 如果您並未設定報表伺服器資料庫，報表伺服器便無法運作，而且您應該在升級之前移除它。  
  
 如需有關解除安裝[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]，請參閱[解除安裝 Reporting Services 2012](http://technet.microsoft.com/library/hh479745.aspx\(v=sql.11\))。 該主題描述如何解除安裝特定版本，而且程序與舊版的程序相似。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 升級問題&#40;Upgrade Advisor&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
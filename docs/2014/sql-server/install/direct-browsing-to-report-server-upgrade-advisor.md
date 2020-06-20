---
title: 直接流覽至報表伺服器（Upgrade Advisor） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 3d2814a4-318a-45ed-b093-1e852fab561f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9a12f39bc399e2c46e61fc290bb20ad2c43e4de9
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85012556"
---
# <a name="direct-browsing-to-report-server-upgrade-advisor"></a>直接瀏覽報表伺服器 (Upgrade Advisor)
  Upgrade Advisor 偵測到您目前的安裝 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 正在直接流覽至報表伺服器虛擬目錄。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]SharePoint 模式。|  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>描述  
 Upgrade Advisor 偵測到您目前的安裝 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 正在直接流覽至報表伺服器虛擬目錄，例如**HTTP:// \<server name> /ReportServer**。 在目前 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 版本中不支援。  
  
> [!NOTE]  
>  此規則是警告，升級未遭到封鎖。  
  
## <a name="corrective-action"></a>更正動作  
 使用文件庫的 SharePoint 使用者介面流覽，或使用**HTTP:// \<server name> /sharepoint site>/_vti_bin/reportserver**。  
  
  

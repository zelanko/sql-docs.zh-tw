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
manager: craigg
ms.openlocfilehash: 6945828b2eba829c32d717c13393c9fbda4fc43e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "71952215"
---
# <a name="direct-browsing-to-report-server-upgrade-advisor"></a>直接瀏覽報表伺服器 (Upgrade Advisor)
  Upgrade Advisor 偵測到您目前的[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]安裝正在直接流覽至報表伺服器虛擬目錄。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]SharePoint 模式。|  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>描述  
 Upgrade Advisor 偵測到您目前的[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]安裝正在直接流覽至報表伺服器虛擬目錄，例如**HTTP://\<伺服器名稱>/reportserver**。 在目前 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 版本中不支援。  
  
> [!NOTE]  
>  此規則是警告，升級未遭到封鎖。  
  
## <a name="corrective-action"></a>更正動作  
 使用文件庫的 SharePoint 使用者介面流覽，或使用**HTTP://\<伺服器名稱>/sharepoint 網站>/_vti_bin/reportserver**。  
  
  

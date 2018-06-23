---
title: 直接瀏覽報表伺服器 (Upgrade Advisor) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3d2814a4-318a-45ed-b093-1e852fab561f
caps.latest.revision: 6
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: f08bc5d25eed160b814bfcdc255e1f198836da2b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36023031"
---
# <a name="direct-browsing-to-report-server-upgrade-advisor"></a>直接瀏覽報表伺服器 (Upgrade Advisor)
  Upgrade Advisor 偵測到您目前安裝的[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]直接瀏覽報表伺服器虛擬目錄。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式。|  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>描述  
 Upgrade Advisor 偵測到您目前安裝的[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]直接瀏覽報表伺服器虛擬目錄，例如**http://\<伺服器名稱 > / ReportServer**。 在目前 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 版本中不支援。  
  
> [!NOTE]  
>  此規則是警告，升級未遭到封鎖。  
  
## <a name="corrective-action"></a>更正動作  
 瀏覽文件庫中使用的 SharePoint 使用者介面或使用**http://\<伺服器名稱 > / sharepoint 網站 >/_vti_bin/reportserver**。  
  
  
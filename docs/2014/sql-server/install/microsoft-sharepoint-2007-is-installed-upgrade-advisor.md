---
title: 已安裝 Microsoft SharePoint 2007 (Upgrade Advisor) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6f1da295-d9b7-4948-99d3-ebd3587337c6
caps.latest.revision: 6
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: 8cc8140166df0a84f1097d2287060baf3a4b41d9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36037607"
---
# <a name="microsoft-sharepoint-2007-is-installed-upgrade-advisor"></a>已安裝 Microsoft SharePoint 2007 (Upgrade Advisor)
  Upgrade Advisor 偵測到不支援的 SharePoint 產品與技術版本。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式。|  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>描述  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 無法升級或安裝於 SharePoint 2007。 升級遭到封鎖。  
  
## <a name="corrective-action"></a>更正動作  
 若要繼續升級，您必須解除安裝 SharePoint 2007 或將 SharePoint 2007 升級為 SharePoint 2010 產品。 升級 SharePoint 安裝之後，請重新執行 Upgrade Advisor，以便確認沒有其他升級問題。  
  
 您無法直接從 SharePoint 2007 升級為 SharePoint 2013。 但是您可以進行稱為「雙躍點」(Double-hop) 的資料庫附加作業，從 Office SharePoint Server 2007 升級至 SharePoint Server 2010，然後再從 SharePoint Server 2010 升級至 SharePoint Server 2013。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 升級問題&#40;Upgrade Advisor&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
---
title: 偵測的 SQL Server 2005 報表伺服器 Web 服務群組 (Upgrade Advisor) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- deployment [Reporting Services]
ms.assetid: 699d24eb-7756-4b41-9294-ef1a94b2f267
caps.latest.revision: 15
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 83f19122e9c6846de6465fba84226076ce7fec9b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37265704"
---
# <a name="sql-server-2005-report-server-web-service-group-detected-upgrade-advisor"></a>偵測到 SQL Server 2005 報表伺服器 Web 服務群組 (Upgrade Advisor)
  Upgrade Advisor 偵測到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體相關聯[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]報表伺服器 Web 服務群組。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式|  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>描述  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 不會使用[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]報表伺服器 Web 服務群組。 當您從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 升級為 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 時，系統將在升級期間刪除這個服務群組，而且不會保留這個群組的自訂存取控制清單 (ACL) 或屬於這個群組的使用者。  
  
## <a name="corrective-action"></a>更正動作  
 升級之前，請先備份任何自訂 ACL 或屬於 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 報表伺服器 Web 服務群組的使用者。 若要這樣做，您可以使用**Icacls.exe**中的命令列工具[!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)]SP2 和更新版本或之前的 Windows 作業系統中的 Cacls.exe 命令列工具[!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)]SP2。 如需有關這些工具之語法的詳細資訊，請參閱 Windows 產品文件集。 安裝程式成功完成之後，請將自訂 ACL 或使用者套用至報表伺服器執行個體的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 報表伺服器 Windows 群組。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]報表伺服器 Windows 群組的形式為 SQLServerReportServerUser$\<*computer_name*>$\<*instance_name*>。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 升級問題&#40;Upgrade Advisor&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  

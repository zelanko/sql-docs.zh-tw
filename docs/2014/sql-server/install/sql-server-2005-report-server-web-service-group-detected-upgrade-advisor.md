---
title: 已偵測到 SQL Server 2005 報表伺服器 Web 服務群組（Upgrade Advisor） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- deployment [Reporting Services]
ms.assetid: 699d24eb-7756-4b41-9294-ef1a94b2f267
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: bfeff5eae569b481edfcc1cacc89c26e44edaece
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952367"
---
# <a name="sql-server-2005-report-server-web-service-group-detected-upgrade-advisor"></a>偵測到 SQL Server 2005 報表伺服器 Web 服務群組 (Upgrade Advisor)
  Upgrade Advisor 偵測到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 實例與 @no__t 1 報表伺服器 Web 服務群組相關聯。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式|  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>描述  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 不會使用 @no__t 2 報表伺服器 Web 服務群組。 當您從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 升級為 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 時，系統將在升級期間刪除這個服務群組，而且不會保留這個群組的自訂存取控制清單 (ACL) 或屬於這個群組的使用者。  
  
## <a name="corrective-action"></a>更正動作  
 升級之前，請先備份任何自訂 ACL 或屬於 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 報表伺服器 Web 服務群組的使用者。 若要這麼做，您可以使用 [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] SP2 和更新版本中的**Icacls**命令列工具，或 @no__t 2 SP2 之前 Windows 作業系統中的 Cacls 命令列工具。 如需有關這些工具之語法的詳細資訊，請參閱 Windows 產品文件集。 安裝程式成功完成之後，請將自訂 ACL 或使用者套用至報表伺服器執行個體的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 報表伺服器 Windows 群組。 @No__t 0 報表伺服器 Windows 群組會採用 SQLServerReportServerUser $ @no__t *-1 電腦*的形式，>$ @ no__t-4*instance_name*>。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 升級問題&#40;upgrade Advisor&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  

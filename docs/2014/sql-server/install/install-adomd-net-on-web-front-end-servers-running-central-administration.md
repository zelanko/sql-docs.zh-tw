---
title: 執行中央系統管理的 Web 前端伺服器上安裝 ADOMD.NET |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: c2372180-e847-4cdb-b267-4befac3faf7e
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: a9a260261a2078ac732c9b3eba2b0c1a9f335cf4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48165880"
---
# <a name="install-adomdnet-on-web-front-end-servers-running-central-administration"></a>在執行管理中心的 Web 前端伺服器上安裝 ADOMD.NET
  如果您將 PowerPivot for SharePoint 安裝到具有管理中心拓撲的伺服器陣列中 (沒有 Excel Services 或 PowerPivot for SharePoint)，若要完整存取 PowerPivot 管理儀表板中的內建報表，請下載及安裝 Microsoft ADOMD.NET 用戶端程式庫。 儀表板中的某些報表會使用 ADOMD.NET 來存取內部資料，這些資料會提供關於在伺服陣列中 PowerPivot 查詢處理和伺服器健全狀況的報告資料。  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2010  
  
 若為 SharePoint 2013，提供者內含在 SQL Server 功能套件中。 如需如何下載 spPowerPivot.msi 的詳細資訊，請參閱[Microsoft SQL Server 2014 功能套件](http://www.microsoft.com/download/details.aspx?id=35577)  
  
### <a name="download-and-install-the-client-library"></a>下載和安裝用戶端文件庫  
  
1.  在  [SQL Server 2014 功能套件頁面](http://go.microsoft.com/fwlink/?LinkID=296473)，尋找 Microsoft ADOMD.NET。  
  
2.  下載 `SQL_AS_ADOMD.msi` 安裝程式的 x64 封裝。  
  
3.  執行 .msi 以安裝程式庫。  
  
4.  當安裝完成之後，重設 IIS。 開啟系統管理命令提示字元並輸入**IISRESET**。  
  
### <a name="verify-installation"></a>確認安裝  
  
1.  移至 Windows\Assembly。  
  
2.  以滑鼠右鍵按一下 Microsoft.AnalysisServices.AdomdClient，然後選取**屬性**。  
  
3.  按一下 **[版本]**。  
  
4.  請確認該版本包含 12.00。\<組建編號 > 且描述為 Microsoft.AnalysisService.AdomdClient。  
  
## <a name="see-also"></a>另請參閱  
 [PowerPivot 管理儀表板和使用量資料](../../analysis-services/power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data.md)  
  
  

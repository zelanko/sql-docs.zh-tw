---
title: "SQL Server Integration Services |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- SSIS
helpviewer_keywords:
- SSIS
- DTS [Integration Services]
- SQL Server Integration Services
- Integration Services
- DTS [Integration Services], about Integration Services
- data integration [Integration Services]
- Data Transformation Services
ms.assetid: c4398655-5657-4ae4-a690-a380790fe84f
caps.latest.revision: 51
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: e76675099ab290d29231d434eb74e92b613185b7
ms.openlocfilehash: 3c07bf1f605d23ffb4ffdd256ba446d215a046ab
ms.contentlocale: zh-tw
ms.lasthandoff: 09/29/2017

---
# <a name="sql-server-integration-services"></a>SQL Server Integration Services

 > 如需舊版的 SQL Server 相關的內容，請參閱[SQL Server Integration Services](https://msdn.microsoft.com/en-US/library/ms141026(SQL.120).aspx)。

[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 是可建立企業級資料整合和資料轉換方案的平台。 您可利用下列方式使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 解決複雜的商務問題：複製或下載檔案、傳送電子郵件訊息以回應事件、更新資料倉儲、清理和採礦資料，以及管理 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 物件和資料。 這些封裝可單獨使用或搭配其他封裝使用，以因應複雜的商務需求。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 可從各種來源 (如 XML 資料檔案、一般檔案與關聯式資料來源) 擷取與轉換資料，然後再將該資料載入一個或多個目的地。<br /><br /> [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包含一組豐富的內建工作和轉換；建構封裝的工具；以及執行和管理封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務。 您可使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 圖形工具建立方案，而不需要撰寫任何程式碼；或者，您也可以撰寫擴充 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 物件模型，以程式設計方式建立封裝及撰寫自訂工作和其他封裝物件。

## <a name="try-sql-server-and-sql-server-integration-services"></a>嘗試使用 SQL Server 和 SQL Server Integration Services
- [![從評估中心下載](../includes/media/download2.png)](http://go.microsoft.com/fwlink/?LinkID=829477)[下載 SQL Server 2017 或 2016年](https://www.microsoft.com/evalcenter/evaluate-sql-server)
- [![從 Evaluation Center 下載](../includes/media/download2.png)](../ssdt/download-sql-server-data-tools-ssdt.md) [下載 SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)
- [![從 Evaluation Center 下載](../includes/media/download2.png)](../ssms/download-sql-server-management-studio-ssms.md) [下載 SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)

##  <a name="infotipsql-servermediainfo-tippng-get-help"></a>![info_tip](../sql-server/media/info-tip.png) 取得說明
 
- [適用於 SSIS 的 MSDN 論壇中詢問問題](https://social.msdn.microsoft.com/Forums/en-us/home?forum=sqlintegrationservices)
- [SSDT 和 SSMS-MSDN 論壇中詢問問題](https://social.msdn.microsoft.com/Forums/en-US/home?forum=sqltool)
- [堆疊溢位 (標記*ssis*)-詢問的問題](http://stackoverflow.com/questions/tagged/ssis)
- [Microsoft Connect - 報告錯誤及要求功能](https://connect.microsoft.com/SQLServer/Feedback)
- [Reddit-SSIS 的一般討論](https://www.reddit.com/r/SQLServer/search?q=ssis&restrict_sr=on)
- [商務使用者的 Microsoft 支援選項](https://support.microsoft.com/gp/support-options-for-business)
- [商務使用者連絡 Microsoft 選項](https://support.microsoft.com/gp/contactus81?Audience=Commercial)


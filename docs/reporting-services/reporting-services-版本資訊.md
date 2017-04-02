---
title: "SSRS 中的 Power BI 報表技術預覽 - 版本資訊 | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-vnext"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4c2f20d7-a9f9-47e3-8dc3-c544a14457e0
caps.latest.revision: 5
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# Reporting Services 版本資訊
 ||  
|-|  
|**[!INCLUDE[applies](../includes/applies-md.md)]**SQL Server Reporting Services 中的 Power BI 報表 2017 年 1 月技術預覽|

本主題描述 SQL Server Reporting Services 中的 Power BI 報表技術預覽的限制與問題。

- 若要了解本版的新功能，請參閱 [Reporting Services 的新功能](../reporting-services/sql-server-reporting-services-ssrs-中的新功能.md)。

 **現在就試試看：**    
   -   [![從 Microsoft 下載中心下載](../analysis-services/media/download.png)](https://go.microsoft.com/fwlink/?linkid=839351) 從 **[Microsoft 下載中心](https://go.microsoft.com/fwlink/?linkid=839351)**下載 SQL Server Reporting Services 中的 Power BI 報表技術預覽，以及 Power BI Desktop (SQL Server Reporting Services)


## <a name="january--2017"></a>2017 年 1 月

### <a name="report-server"></a>報表伺服器

- 現已支援 HTTPS。 2016 年 10 月發行的技術預覽 VM 中沒有這項支援。 如需詳細資訊，請參閱[在原生模式報表伺服器上設定 SSL 連接](../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md)。
   - 必須透過 HTTPS 才能使用 PowerPoint Web 檢視器增益集，並公開其中的 Power BI 報表。
- 現已支援向外延展。 2016 年 10 月發行的技術預覽 VM 中沒有這項支援。 如需詳細資訊，請參閱[設定原生模式報表伺服器向外延展部署](../reporting-services/install-windows/configure a native mode report server scale-out deployment.md)。

### <a name="power-bi-reports"></a>Power BI 報表

- 必須使用 Power BI Desktop (SQL Server Reporting Services) 建立 Power BI 報表才能與 SQL Server Reporting Services 搭配使用。 您可以從評估中心下載 Power BI Desktop (SQL Server Reporting Services)。
- Power BI 報表僅支援對 Analysis Services (表格式或多維度) 的即時連線。
- 不支援自訂的視覺效果。
- 不支援 R 視覺效果。
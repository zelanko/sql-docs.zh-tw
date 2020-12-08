---
title: 支援報表檢視器控制項版本
description: Microsoft 報表檢視器控制項相容於遵循新式支援週期原則的 SQL Server Reporting Services 以及 Power BI 報表伺服器。
author: maggiesMSFT
ms.custom: seo-lt-2019
ms.author: maggies
ms.reviewer: jonhp
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.topic: reference
ms.date: 12/01/2020
ms.openlocfilehash: f6c713d579042425dc863b7d4f942229a091d0c4
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/02/2020
ms.locfileid: "96502692"
---
# <a name="support-for-report-viewer-current-branch-versions"></a>報表檢視器最新分支版本的支援

**_適用對象：Microsoft Report Viewer 150.900.148 版和更新版本_**

**Microsoft Report Viewer 控制項** 與依循 [支援週期原則](https://support.microsoft.com/hub/4095338/microsoft-lifecycle-policy)的 SQL Server Reporting Services 和「Power BI 報表伺服器」相容。 此資訊同時適用於透過 [NuGet](https://www.nuget.org/) \(英文\) 散發的 **ASP.NET** 與 **WinForms** 版本。 透過 [NuGet](https://www.nuget.org/) 可取得所有發行版本。 修補程式、功能或其他更新會向前復原至最新版本。 必須套用最新版本，才能接收變更。 「報表檢視器」會繼續收到 **安全性和重大更新**，如有任何支援政策變更，將會至少提前一年通知。

如需 Report Viewer 控制項的版本歷程記錄，請參閱下列連結：

- [Windows Forms](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.Winforms/) \(英文\)
- [ASP.NET Web Forms](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.WebForms/) \(英文\)

## <a name="application-server-and-report-server-combinations"></a>應用程式伺服器與報表伺服器組合

報表檢視器控制項的某些功能需仰賴作業系統的預設行為。 因此，其可能需要同時針對用戶端 (執行報表檢視器控制項的應用程式伺服器) 與伺服器 (執行 Reporting Services) 執行相同的版本。 支援下列應用程式伺服器與報表伺服器的組合：

| 應用程式伺服器 | 報表伺服器 |
| :----------------- | :------ |
| Windows Server 2012 | Windows Server 2012 |
| Windows Server 2012 | Windows Server 2012 R2 |
| Windows Server 2012 R2 | Windows Server 2012 R2 |
| Windows Server 2012 R2 | Windows Server 2012 |
| Windows Server 2016 和更新版本 | Windows Server 2016 和更新版本 |

## <a name="next-steps"></a>後續步驟

如需報表檢視器控制項的詳細資訊，請參閱[開始使用報表檢視器控制項整合 Reporting Services](integrating-reporting-services-using-reportviewer-controls-get-started.md)。

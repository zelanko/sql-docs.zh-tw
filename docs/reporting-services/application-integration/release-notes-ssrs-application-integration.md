---
title: SSRS 報表檢視器控制項的版本資訊
ms.date: 09/20/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.topic: reference
ms.assetid: 112e0240-351d-46a9-98c7-2be09f26ac60
ms.reviewer: maghan
author: RhysSchmidtke
ms.author: rhys
ms.openlocfilehash: 1528358c8aff5d6e99869f0f4f8c1676ee2d5e75
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2019
ms.locfileid: "67730903"
---
# <a name="release-notes-for-the-report-viewer-controls-for-webforms-and-winforms-of-ssrs"></a>WebForms 和 WinForms 的 SSRS 的報表檢視器控制項的版本資訊

這些是 WebForms 和 WinForms、 相關的報表檢視器控制項的版本資訊[!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (SSRS)。

Ssrs 的版本資訊，請參閱[版本資訊的 SQL Server Reporting Services (SSRS) 2017年和更新版本](../release-notes-reporting-services.md)。

## <a name="15013580"></a>150.1358.0
| 變更描述 | 詳細資料 |
| :----------------- | :------ |
| 錯誤修正 | 還原專案參考中移除 Microsoft.ReportViewer.Design 組件的變更。 |
|           | 其他變更的一部分，兩個組件已從 15.0 版本變更為 15.3。 這已還原。 |
| &nbsp; | &nbsp; |

## <a name="15013570"></a>150.1357.0
| 變更描述 | 詳細資料 |
| :----------------- | :------ |
| 錯誤修正  | 高 DPI 監視器的適當列印預覽 |
|            | 列印對話方塊會顯示外部可見的空間 |
|            | 大量的參數產生參數捲軸以及無法正常運作的下拉式清單 |
|            | 已修正的問題，使用 Null 和日期時間參數 |
|            | 更新的 JQuery 版本 3.3.1 |
|            | 已修正與 HTML 轉譯中的 tablix 資料格重疊 |
|            | 移除專案參考以消除錯誤新增至專案的 VS 組件的設計階段 |
|            | 協助工具修正錄製旁白的那只會針對作用中的項目工具列 |
| &nbsp; | &nbsp; |

## <a name="15900148"></a>15.900.148

| 變更描述 | 詳細資料 |
| :----------------- | :------ |
| 修正防止透過 **Server.LoadReportDefinition** 載入且無參數報表的錯誤 (Bug)。 | &nbsp; |
| WebForms 報表檢視器控制項。 | 支援 RTL 頁面 (使用 *direction: rtl;* CSS 屬性變更文字流程的頁面) 中的內嵌。<br/><br/>透過 *IReportViewerMessages5* 當地語系化介面來支援自訂列印對話方塊文字。<br/><br/>已改善協助工具支援。<br/><br/>&bull; &nbsp; &nbsp; [報表檢視器控制項的 WebForms 的 NuGet 套件](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.Webforms/150.900.148) |
| WinForms 報表檢視器控制項。 | 修正以高 DPI 模式執行應用程式時的列印。<br/><br/>&bull; &nbsp; &nbsp; [報表檢視器控制項的 WinForms 的 NuGet 套件](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.Winforms/150.900.148) |
| &nbsp; | &nbsp; |

## <a name="next-steps"></a>後續步驟

報表檢視器控制項的[入門](integrating-reporting-services-using-reportviewer-controls-get-started.md)。

更多問題嗎？ [試試 Reporting Services 論壇](https://go.microsoft.com/fwlink/?LinkId=620231)。

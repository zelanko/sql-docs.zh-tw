---
title: 報表檢視器控制項的版本資訊
description: WebForms 和 WinForms 的報表檢視器控制項版本資訊，與 Reporting Services 有關。
ms.date: 01/16/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.custom: seo-lt-2019
ms.topic: reference
ms.assetid: 112e0240-351d-46a9-98c7-2be09f26ac60
ms.reviewer: maggies
author: RhysSchmidtke
ms.author: rhys
ms.openlocfilehash: 5ee9bd80519e9dc9d75bb78a98b548b2a60ef247
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "76259376"
---
# <a name="release-notes-for-report-viewer-controls-for-webforms-and-winforms-of-ssrs"></a>SSRS WebForms 和 WinForms 的報表檢視器控制項版本資訊

這些是 WebForms 和 WinForms 的報表檢視器控制項版本資訊，與 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (SSRS) 相關。

如需 SSRS 的版本資訊，請參閱 [SQL Server Reporting Services (SSRS) 2017 和更新版本的版本資訊](../release-notes-reporting-services.md)。

## <a name="15014000"></a>150.1400.0
| 變更描述 | 詳細資料 |
| :----------------- | :------ |
| 錯誤修正 | 修正了檢視器控制項不會在設計模式中載入的問題。 |
| &nbsp; | &nbsp; |

## <a name="15013580"></a>150.1358.0
| 變更描述 | 詳細資料 |
| :----------------- | :------ |
| 錯誤修正 | 已還原從專案參考中移除 Microsoft.ReportViewer.Design 組件的變更。 |
|           | 在進行其他變更時，兩個組件的版本會從 15.0 變更為 15.3。 已還原此變更。 |
| &nbsp; | &nbsp; |

## <a name="15013570"></a>150.1357.0
| 變更描述 | 詳細資料 |
| :----------------- | :------ |
| 錯誤修正  | 適用於高 DPI 監視器的適當預覽列印 |
|            | [列印] 對話方塊會顯示在可見空間之外 |
|            | 大量參數會導致參數捲軸和下拉式清單無法正常運作 |
|            | 已修正 Null 和日期時間參數的問題 |
|            | 已將 JQuery 更新至版本 3.3.1 |
|            | 已修正 HTML 轉譯中 Tablix 資料格重疊的問題 |
|            | 移除設計階段專案參考以避免將錯誤的 VS 組件新增至專案 |
|            | 工具列的協助工具修正程式僅針對作用中項目製作旁白 |
| &nbsp; | &nbsp; |

## <a name="150900148"></a>150.900.148

| 變更描述 | 詳細資料 |
| :----------------- | :------ |
| 修正防止透過 **Server.LoadReportDefinition** 載入且無參數報表的錯誤 (Bug)。 | &nbsp; |
| WebForms 報表檢視器控制項。 | 支援 RTL 頁面 (使用 *direction: rtl;* CSS 屬性變更文字流程的頁面) 中的內嵌。<br/><br/>透過 *IReportViewerMessages5* 當地語系化介面來支援自訂列印對話方塊文字。<br/><br/>已改善協助工具支援。<br/><br/>&bull; &nbsp; &nbsp; [WebForms 的報表檢視器控制項適用的 NuGet 套件](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.Webforms/150.900.148) |
| WinForms 報表檢視器控制項。 | 修正以高 DPI 模式執行應用程式時的列印。<br/><br/>&bull; &nbsp; &nbsp; [WinForms 的報表檢視器控制項適用的 NuGet 套件](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.Winforms/150.900.148) |
| &nbsp; | &nbsp; |

## <a name="next-steps"></a>後續步驟

報表檢視器控制項的[入門](integrating-reporting-services-using-reportviewer-controls-get-started.md)。

更多問題嗎？ [試試 Reporting Services 論壇](https://go.microsoft.com/fwlink/?LinkId=620231)。

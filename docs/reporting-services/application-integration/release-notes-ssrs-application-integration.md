---
title: SSRS 報表檢視器控制項的版本資訊
ms.date: 09/20/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.topic: reference
ms.assetid: 112e0240-351d-46a9-98c7-2be09f26ac60
ms.reviewer: maggies
author: RhysSchmidtke
ms.author: rhys
ms.openlocfilehash: d6c7130e45e535ad1849bed5713313bf6f89020f
ms.sourcegitcommit: 071065bc5433163ebfda4fdf6576349f9d195663
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/03/2019
ms.locfileid: "71923806"
---
# <a name="release-notes-for-the-report-viewer-controls-for-webforms-and-winforms-of-ssrs"></a>SSRS 的 WebForms 和 WinForms 之報表檢視器控制項的版本資訊

這些是 WebForms 和 WinForms 之報表檢視器控制項的版本資訊，與 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] （SSRS）相關。

如需 SSRS 的版本資訊，請參閱[SQL Server Reporting Services （SSRS）2017和更新版本的版本](../release-notes-reporting-services.md)資訊。

## <a name="15013580"></a>150.1358.0
| 變更描述 | 詳細資料 |
| :----------------- | :------ |
| 錯誤修正 | 已還原從專案參考中移除 Microsoft ReportViewer. 設計元件的變更。 |
|           | 在進行其他變更時，會將兩個元件從15.0 版本變更為15.3。 這已經還原。 |
| &nbsp; | &nbsp; |

## <a name="15013570"></a>150.1357.0
| 變更描述 | 詳細資料 |
| :----------------- | :------ |
| 錯誤修正  | 適用于高 DPI 監視器的適當預覽列印 |
|            | [列印] 對話方塊會顯示在可見的空間之外 |
|            | 大量參數導致參數捲軸和下拉式清單無法正常運作 |
|            | 已修正 Null 和日期時間參數的問題 |
|            | 已將 JQuery 更新為版本3.3。1 |
|            | 已修正 HTML 轉譯中 tablix 資料格的重迭 |
|            | 移除設計階段專案參考，以避免將錯誤的 VS 元件新增至專案 |
|            | 協助工具修正工具列僅適用于作用中專案的敘述 |
| &nbsp; | &nbsp; |

## <a name="15900148"></a>15.900.148

| 變更描述 | 詳細資料 |
| :----------------- | :------ |
| 修正防止透過 **Server.LoadReportDefinition** 載入且無參數報表的錯誤 (Bug)。 | &nbsp; |
| WebForms 報表檢視器控制項。 | 支援 RTL 頁面 (使用 *direction: rtl;* CSS 屬性變更文字流程的頁面) 中的內嵌。<br/><br/>透過 *IReportViewerMessages5* 當地語系化介面來支援自訂列印對話方塊文字。<br/><br/>已改善協助工具支援。<br/><br/>&bull; &nbsp; &nbsp; [NuGet 封裝，適用于 WebForms 的報表檢視器控制項](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.Webforms/150.900.148) |
| WinForms 報表檢視器控制項。 | 修正以高 DPI 模式執行應用程式時的列印。<br/><br/>&bull; &nbsp; &nbsp; [NuGet 封裝，適用于 WinForms 的報表檢視器控制項](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.Winforms/150.900.148) |
| &nbsp; | &nbsp; |

## <a name="next-steps"></a>後續步驟

報表檢視器控制項的[入門](integrating-reporting-services-using-reportviewer-controls-get-started.md)。

更多問題嗎？ [試試 Reporting Services 論壇](https://go.microsoft.com/fwlink/?LinkId=620231)。

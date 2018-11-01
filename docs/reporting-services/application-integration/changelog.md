---
title: Reporting Services 報表檢視器控制項的變更記錄
ms.date: 09/19/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.topic: reference
ms.assetid: 112e0240-351d-46a9-98c7-2be09f26ac60
author: RhysSchmidtke
ms.author: rhys
ms.openlocfilehash: 57eca1ced359ec08dc9b64f6840d0eadf1fb3f3e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47771377"
---
# <a name="changelog-for-the-report-viewer-controls"></a>報表檢視器控制項的變更記錄

此變更記錄會追蹤 WinForms and WebForms 報表檢視器控制項的版本。

## <a name="15900148"></a>15.900.148
具有此更新
 - 修正防止透過 Server.LoadReportDefinition 載入且無參數報表的Bug

[WebForms](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.Webforms/150.900.148) 報表檢視器控制項
 - 支援 RTL 頁面 (使用 *direction: rtl;* CSS 屬性變更文字流程的頁面) 中的內嵌。
 - 透過 *IReportViewerMessages5* 當地語系化介面來支援自訂列印對話方塊文字。
 - 已改善協助工具支援。

[WinForms](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.Winforms/150.900.148) 報表檢視器控制項
 - 修正以高 DPI 模式執行應用程式時的列印。

## <a name="next-steps"></a>後續步驟

報表檢視器控制項的[入門](integrating-reporting-services-using-reportviewer-controls-get-started.md)  
更多問題嗎？ [試試 Reporting Services 論壇](https://go.microsoft.com/fwlink/?LinkId=620231)

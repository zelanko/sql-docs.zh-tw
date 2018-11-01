---
title: SQL Server Reporting Services (SSRS) 2017 和更新版本的變更記錄檔 | Microsoft Docs
ms.date: 08/31/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
author: casualoak
ms.author: edugonz
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 2fa40e17381622862ea2a5b5e6fac594f6a42f6a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47728769"
---
# <a name="change-log-for-sql-server-reporting-services-ssrs-2017-and-later"></a>SQL Server Reporting Services (SSRS) 2017 和更新版本的變更記錄檔

[!INCLUDE [ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2017-and-later](../includes/ssrs-appliesto-2017-and-later.md)] 

本文說明 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中的變更。 

## <a name="sql-server-2017-reporting-services"></a>SQL Server 2017 Reporting Services 

### <a name="version-140600906-released-september-12-2018"></a>14.0.600.906 版，發行日期：2018 年 9 月 12 日

這個錯誤 (Bug) 已修正：

- 未傳回正確 Cookie 資訊的自訂驗證

### <a name="version-140600892-released-august-31-2018"></a>14.0.600.892 版，發行日期：2018 年 8 月 31 日

已修正這些錯誤 (Bug)：

- 當 rc:Toolbar=False 且它有長文字時，矩形內的文字方塊會導致矩形無法垂直成長 
- 若 pageHeight 小於 0.5 英吋，則不會縮放文字大小 
- 搭配 CRM 使用時，SSRS 類別目錄資料庫中的死結 
- 當在報告中向下捲動時，垂直對齊資料行標頭不正確地顯示 
- 被新增到 SCOM 回報角色的使用者將無法存取 SSRS Web 入口網站 
- 泰文字元未在 PDF 中正確匯出 
- 瀏覽器角色行為變更 
- rc:Toolbar=false 無法在 Express 版本中使用 
- 參數提示區域中缺少垂直捲軸 
- 已更新行動報表執行階段 

### <a name="version-140600744-released-april-25-2018"></a>14.0.600.744 版，發行日期：2018 年 4 月 25 日 

已修正這些錯誤 (Bug)：

- 資料驅動訂閱頁面建立好之後，它便不會顯示 [傳遞選項]
- SSRS 2012 升級至 SSRS 2017 會造成 RSManagement 每隔幾秒便擲回例外狀況
- 無法變更 IE11 中的多重值參數預設值
- 每當執行共用的排程時，排程便會是空的

### <a name="version-140600689-released-february-28-2018"></a>14.0.600.689 版，發行日期：2018 年 2 月 28 日

已修正這些錯誤 (Bug)：

- 編輯報表參數的屬性之後，其在連結的報表中的可見性會被還原
- URL 參數 rc:Toolbar=false 無法在 Express 版本中使用
- Textbox 中包含設定為 False 的 CanGrow 屬性之運算式會導致不顯示值
- 在安裝程式中新增產品金鑰的 [深入了解] 連結
- 含自訂表單驗證的 Web 入口網站會忽略變動到期 Cookie
- 如果資料列的內容是空的，匯出到 Word 會建立不相等的資料列高度

### <a name="version-140600594-released-january-9-2018"></a>14.0.600.594 版，發行日期：2018 年 1 月 9 日

安全性更新

### <a name="version-140600490-released-november-1-2017"></a>14.0.600.490 版，發行日期：2017 年 11 月 1 日

這個錯誤 (Bug) 已修正：

- 已解決 SKU 升級問題

### <a name="version-140600451-released-september-30-2017"></a>14.0.600.451 版，發行日期：2017 年 9 月 30 日 

最初發行

## <a name="next-steps"></a>後續步驟

[Reporting Services (SSRS) 中的新功能](what-s-new-in-sql-server-reporting-services-ssrs.md)   

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)

---
title: 版本資訊 (SSRS) 2017年和更新版本 |Microsoft Docs
ms.date: 02/18/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.reviewer: maggies
author: casualoak
ms.author: rhys
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions'
ms.openlocfilehash: 8767640e2ad0a7b71bb7977ab6eb997892845403
ms.sourcegitcommit: eacc2d979f1f13cfa07e0aa4887eb9d48824b633
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2019
ms.locfileid: "67533835"
---
# <a name="release-notes-for-sql-server-reporting-services-ssrs-2017-and-later"></a>SQL Server Reporting Services (SSRS) 2017 與更新版本的版本資訊

[!INCLUDE [ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2017-and-later](../includes/ssrs-appliesto-2017-and-later.md)]

這篇文章說明中的變更[!INCLUDE[ssnoversion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] (SSRS)，對於 2017年和更新版本的版本。

報表檢視器控制項的版本資訊，請參閱[Release Notes for 報表檢視器控制項 WebForms 和 WinForms 的 SSRS](application-integration/release-notes-ssrs-application-integration.md)。

<!--
We are "standardizing" all our 'Release Notes' style articles:

  - File names:   'release-notes-[TechArea-Name].md'


  - Content format:   2-column tables.  No longer using bullet lists.

    - Ideally, the 'Details' column should contain a link to another SSRS documentation article wherein the particular issue fix is discussed in any way.  Or if there is more to say beyond one sentence, the other sentences of elaboration would go into the 'Details' column.


  - H2 header names are kept short, for better display.


  - Try to keep all Release Notes in one .md file.  Avoid having multiple R.N. files whose names differ only by version or date.

    - Seriously consider erasing info about ancient releases that are so old that nobody cares about them anymore.  If you really want to retain ancient info, consider doing so in an HTML comment at the end of the .md file, just in case a Microsoft employee needs to re-examine ancient info.  In any case, this file cannot get ever longer, and some deletion or hiding of oldest info must eventually occur.


  - Do use '::: moniker range=' zones when version 2017 is no longer the only version represented inside this .md file.

    - Use the '=' operator on the moniker, not the '>=' operator.
    - In contrast, in our 'Whats New' articles we do use the '>=', rather than '='.

GeneMi, DevOps = 1467988 (MsEng > TechnicalContent) , 2019/03/19
-->

## <a name="1406001274-20190701"></a>2019/07/01 14.0.600.1274

| 已修正的問題 | 詳細資料 |
| :---------- | :------ |
| 安全性更新 | &nbsp; |
| 無法選取工作日建立共用的每週排程時 | &nbsp; |
| 報表不會顯示換行字元正確 Word 格式 | &nbsp; |
| System Center Operations Manager(SCOM) 2019 沒有較長的運作方式，使用最新的 SSRS 2017 升級 | &nbsp; |
| 叫用授權延伸模組共用資料集時，發生錯誤 | &nbsp; |
| 變更預存程序 GetAllProperties SSRS 2017 及 PBIRS，這會導致 Web 服務端點 ReportingService2010.GetProperties 方法無法取得連結報表中的任何資料的邏輯 | &nbsp; |
| 按一下方格內的項目時，就會消失在行動報表中的簡單格線資料列標頭 | &nbsp; |
| 無法使用資料驅動訂閱參數中的 [日期] 欄位 | &nbsp; |
| 巢狀的 tablix 會顯示小字型或部分的字型，在 SSRS 2016 和更新版本 | &nbsp; |
| 使用日期時間參數發生錯誤的訂用帳戶之後以不同的地區設定編輯訂用帳戶的使用者 | &nbsp; |
| 使用 Null 傳遞延伸模組來建立資料驅動訂閱的 「 發生傳遞錯誤 」 發生失敗 | &nbsp; |
| URL 編碼不正確，Excel\Word 格式設定值時 | &nbsp; |

## <a name="1406001109-20190212"></a>14.0.600.1109，2019/02/12

| 已修正的問題 | 詳細資料 |
| :---------- | :------ |
| 修改訂閱之後，「快取報表快照集排程」變更為「報表特定排程」。 | &nbsp; |
| rc:Toolbar=false 無法在 Express 版本中使用。 | &nbsp; |
| 將分頁報表匯出為 PDF 時，特定泰文字元的轉譯會發生錯誤。 | &nbsp; |
| 在已完成資料驅動訂閱的通知期間發生鎖死。 | &nbsp; |
| 使用 rc:Toolbar=False 參數時，在特定情況下不會顯示內嵌影像。 | &nbsp; |
| 無法針對使用串聯參數的報表建立資料驅動訂閱。 | &nbsp; |
| 無法編輯設有無效間隔的訂用帳戶。 | &nbsp; |
| 安全性更新。 | &nbsp; |
| 未顯示連結的報表 UI。 | &nbsp; |
| 含巢狀 Tablix 控制項的特定分頁報表中，字型有誤。 | &nbsp; |
| 空白字元不正確地加入包含 tablix 資料區之特定編頁報表。 | &nbsp; |
| 展開行動報表的簡單資料格時，標頭資料列會消失。 | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="140600906-20180912"></a>14.0.600.906，2018/09/12

已修正下列問題：

| 已修正的問題 | 詳細資料 |
| :---------- | :------ |
| 未傳回正確 Cookie 資訊的自訂驗證。 | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="140600892-20180831"></a>14.0.600.892，2018/08/31

| 已修正的問題 | 詳細資料 |
| :---------- | :------ |
| 當 rc:Toolbar=False 且它有長文字時，矩形內的文字方塊會導致矩形無法垂直成長。 | &nbsp; |
| 若 pageHeight 小於 0.5 英吋，則不會縮放文字大小。 | &nbsp; |
| CRM 搭配使用時，就會在 SSRS 類別目錄資料庫中發生死結。 | &nbsp; |
| 當在報告中向下捲動時，垂直對齊資料行標頭不正確地顯示。 | &nbsp; |
| 新增至 System Center Operations Manager 報表的角色的使用者可以封鎖至 SSRS web 入口網站的存取。 | &nbsp; |
| 泰文字元未正確匯出至 PDF。 | &nbsp; |
| 瀏覽器角色行為變更。 | &nbsp; |
| rc:Toolbar=false 無法在 Express 版本中使用。 | &nbsp; |
| 遺漏參數提示區域中的垂直捲軸。 | &nbsp; |
| 已更新行動報表執行階段。 | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="140600744-20180425"></a>14.0.600.744，2018/04/25

| 已修正的問題 | 詳細資料 |
| :---------- | :------ |
| 資料驅動訂閱頁面建立好之後，它便不會顯示 [傳遞選項]。 | &nbsp; |
| SSRS 2012 升級至 SSRS 2017 會造成 RSManagement 每隔幾秒便擲回例外狀況。 | &nbsp; |
| 無法變更 IE11 中的多重值參數預設值。 | &nbsp; |
| 每當執行共用的排程時，排程便會是空的。 | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="140600689-20180228"></a>14.0.600.689，2018/02/28

| 已修正的問題 | 詳細資料 |
| :---------- | :------ |
| 編輯報表參數的屬性之後，它在連結的報表中的可見性會被還原。 | &nbsp; |
| URL 參數 rc:Toolbar=false 無法在 Express 版本中使用。 | &nbsp; |
| 需要運算式在文字方塊中的 cangrow 屬性設定為未顯示的值，則為 false 的結果。 | &nbsp; |
| 在安裝程式中新增產品金鑰的 [深入了解]  連結。 | &nbsp; |
| 含自訂表單驗證的 Web 入口網站會忽略變動到期 Cookie。 | &nbsp; |
| 如果資料列的內容是空的，匯出到 Word 會建立不相等的資料列高度。 | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="140600594-20180109"></a>14.0.600.594，2018/01/09

已實作某些安全性更新程式。

### <a name="140600490-20171101"></a>14.0.600.490，2017/11/01

已解決 SKU 升級問題。

## <a name="140600451-20170930"></a>14.0.600.451，2017/09/30

初始版本。

## <a name="next-steps"></a>後續步驟

[Reporting Services (SSRS) 中的新功能](what-s-new-in-sql-server-reporting-services-ssrs.md)

更多問題嗎？ [嘗試詢問 Reporting Services 論壇](https://go.microsoft.com/fwlink/?LinkId=620231)。

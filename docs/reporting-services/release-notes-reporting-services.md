---
title: Reporting Services 2017 和更新版本的版本資訊 | Microsoft Docs
ms.date: 12/04/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.reviewer: maggies
author: casualoak
ms.author: rhys
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions'
ms.openlocfilehash: 39049ee5a2561821e0a2284ed66b9b04730998bf
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "74834254"
---
# <a name="release-notes-for-sql-server-reporting-services-ssrs-2017-and-later"></a>SQL Server Reporting Services (SSRS) 2017 與更新版本的版本資訊

[!INCLUDE [ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2017-and-later](../includes/ssrs-appliesto-2017-and-later.md)]

本文描述 [!INCLUDE[ssnoversion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] (SSRS) 2017 版和更新版本中的變更。

如需報表檢視器控制項的版本資訊，請參閱 [WebForms 和 WinForms SSRS 的報表檢視器控制項版本資訊](application-integration/release-notes-ssrs-application-integration.md)。

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
## <a name="1406001451-20191113"></a>14.0.600.1451 2019/11/13 

| 已修正的問題 | 詳細資料 |
| :---------- | :------ |
| 安全性更新 | &nbsp; |
| 啟用快照集時，編頁報表不能配合篩選參數正常運作  | &nbsp; |
| 具有瀏覽器角色和預設設定的使用者過去無權下載 Excel 檔案  | &nbsp; |
| 升級期間，從 SQL Server 2016 Reporting Services 升級至 Power BI 報表伺服器失敗 | &nbsp; |
| 從 SQL Server 2012 Reporting Services 升級之後，訂用帳戶失敗，並出現「在郵件標頭中找到不正確字元：','」訊息 | &nbsp; |
| 組態工具：在 [資料庫] 區段取消強制回應視窗將會重新啟動 Reporting Services 服務 | &nbsp; |
| Textbox 控制項的 BorderStyle 屬性運算式並未轉譯成 Excel 格式  | &nbsp; |
| 造成某些報表卡在轉譯同一頁面，始終到不了報表最後一頁的分頁問題 | &nbsp; |

## <a name="1406001274-20190701"></a>2019/07/01 14.0.600.1274

| 已修正的問題 | 詳細資料 |
| :---------- | :------ |
| 安全性更新 | &nbsp; |
| 建立共用每週排程時無法選取工作日 | &nbsp; |
| 報表不會正確顯示 Word 格式的歸位字元 | &nbsp; |
| System Center Operations Manager (SCOM) 2019 不再使用最近的 SSRS 2017 升級 | &nbsp; |
| 叫用共用資料集的授權延伸模組時發生錯誤 | &nbsp; |
| SSRS 2017 和 PBIRS 中預存程序 GetAllProperties 的邏輯變更，造成 Web 服務端點 ReportingService2010.GetProperties 方法無法為連結的報表取得任何資料 | &nbsp; |
| 按一下資料格中的項目時，行動報表中的簡易資料格列標頭會消失 | &nbsp; |
| 無法使用資料驅動訂閱參數中的日期欄位 | &nbsp; |
| 巢狀 Tablix 在 SSRS 2016 和更新版本中顯示小型字型或部分字型 | &nbsp; |
| 在具有不同地區設定的使用者編輯訂用帳戶之後，具有 DateTime 參數錯誤的訂用帳戶出局 | &nbsp; |
| 建立具有 Null 傳遞延伸模組的資料驅動訂閱，因「發生傳遞錯誤」而失敗 | &nbsp; |
| 以 Excel\Word 格式設定值時，URL 編碼不正確 | &nbsp; |

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
| 在某些包含 Tablix 資料區域的編頁報表中，錯誤新增了空白字元。 | &nbsp; |
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
| 與 CRM 一起使用時，SSRS 類別目錄資料庫出現死結。 | &nbsp; |
| 當在報告中向下捲動時，垂直對齊資料行標頭不正確地顯示。 | &nbsp; |
| System Center Operations Manager 報表角色所新增使用者封鎖了對 SSRS 入口網站的存取。 | &nbsp; |
| 泰文字元未正確匯出至 PDF。 | &nbsp; |
| 瀏覽器角色行為變更。 | &nbsp; |
| rc:Toolbar=false 無法在 Express 版本中使用。 | &nbsp; |
| 參數提示區域中遺漏垂直捲軸。 | &nbsp; |
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
| 在文字方塊中將運算式的 CanGrow 屬性設定為 False 會導致不顯示值。 | &nbsp; |
| 在安裝程式中新增產品金鑰的 [深入了解]  連結。 | &nbsp; |
| 含自訂表單驗證的 Web 入口網站會忽略變動到期 Cookie。 | &nbsp; |
| 如果資料列的內容是空的，匯出到 Word 會建立不相等的資料列高度。 | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="140600594-20180109"></a>14.0.600.594，2018/01/09

已實作一些安全性更新。

### <a name="140600490-20171101"></a>14.0.600.490，2017/11/01

已解決 SKU 升級問題。

## <a name="140600451-20170930"></a>14.0.600.451，2017/09/30

初始版本。

## <a name="next-steps"></a>後續步驟

[Reporting Services (SSRS) 中的新功能](what-s-new-in-sql-server-reporting-services-ssrs.md)

更多問題嗎？ [嘗試詢問 Reporting Services 論壇](https://go.microsoft.com/fwlink/?LinkId=620231)。

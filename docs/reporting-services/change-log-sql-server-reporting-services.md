---
title: SQL Server Reporting Services (2017 和更新版本) 的變更記錄檔 | Microsoft Docs
ms.custom: ''
ms.date: 04/26/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: reporting-services
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
author: casualoak
ms.author: edugonz
manager: kfile
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: cab026c9ccad3bfb91416311071e957767c41352
ms.sourcegitcommit: 2e038db99abef013673ea6b3535b5d9d1285c5ae
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/01/2018
ms.locfileid: "39400824"
---
# <a name="change-log-for-sql-server-reporting-services"></a>SQL Server Reporting Services 的變更記錄檔

[!INCLUDE [ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2017-and-later](../includes/ssrs-appliesto-2017-and-later.md)] 

本文說明 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中的變更。 

## <a name="sql-server-2017-reporting-services"></a>SQL Server 2017 Reporting Services 

- *14.0.600.744 版，發行日期：2018 年 4 月 25 日* 
    - 錯誤修正：
        - 資料驅動訂閱頁面建立好之後，它便不會顯示 [傳遞選項]
        - SSRS 2012 升級至 SSRS 2017 會造成 RSManagement 每隔幾秒便擲回例外狀況
        - 無法變更 IE11 中的多重值參數預設值
        - 每當執行共用的排程時，排程便會是空的

- 14.0.600.689 版，發行日期：2018 年 2 月 28 日 
    - 錯誤修正：
        - 編輯報表參數的屬性之後，其在連結的報表中的可見性會被還原
        - URL 參數 rc:Toolbar=false 無法在 Express 版本中使用
        - Textbox 中包含設定為 False 的 CanGrow 屬性之運算式會導致不顯示值
        - 在安裝程式中新增產品金鑰的 [深入了解] 連結
        - 含自訂表單驗證的 Web 入口網站會忽略變動到期 Cookie
        - 如果資料列的內容是空的，匯出到 Word 會建立不相等的資料列高度

- 14.0.600.594 版，發行日期：2018 年 1 月 9 日
    - 安全性更新

- *14.0.600.490 版，發行日期：2017 年 11 月 1 日* 
    - 錯誤修正：
        - 已解決 SKU 升級問題

- *14.0.600.451 發行日期：2017 年 9 月 30 日* 
    - 最初發行

## <a name="next-steps"></a>後續步驟

[Reporting Services (SSRS) 中的新功能](what-s-new-in-sql-server-reporting-services-ssrs.md)   

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)

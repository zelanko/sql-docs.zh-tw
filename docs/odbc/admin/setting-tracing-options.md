---
title: 設定追蹤選項 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio Analyzer tracing [ODBC]
- ODBC data source administrator [ODBC], tracing options
- tracing options [ODBC], ODBC data source administrator
ms.assetid: 44404a79-b716-4bc1-9ffb-70cd8239d237
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 21bee5d903459423a134389e62db844f5f63c9c1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307191"
---
# <a name="setting-tracing-options"></a>設定追蹤選項
**通過「ODBC 資料來源管理員」** 對話方塊的 **「追蹤」** 選項卡,您可以設定追蹤 ODBC 函數呼叫的方式。  
  
## <a name="how-tracing-works"></a>追蹤的工作原理  
 從 **『追蹤』** 選項卡開始追蹤時,驅動程式管理員將記錄所有隨後運行的應用程式的所有ODBC函數調用。 不會記錄在開始追蹤之前運行的應用程式的 ODBC 函數呼叫。 ODBC 函數呼叫記錄在您指定的紀錄檔中。  
  
 僅在單擊「**立即停止跟蹤」 後才會停止。** 請記住,當跟蹤打開時,日誌檔繼續增加,這會影響所有 ODBC 應用程式的性能。  
  
 有關追蹤的詳細資訊,請參閱[追蹤](../../odbc/reference/develop-app/tracing.md)。  
  
### <a name="changes-in-odbc-tracing"></a>ODBC 追蹤的變化  
 在 MDAC 2.7 SP2 之前,ODBC 追蹤只允許在全機範圍內進行,跟蹤捕獲任何標識下運行的所有 ODBC 應用程式的公開詳細資訊。 這包括追蹤可能針對代表其他本地使用者帳戶和內建安全主體(如本地服務和網路服務)創建或運行的進程發生的與 ODBC 相關的活動。  
  
 默認情況下,ODBC 追蹤現在使用每個使用者模式。 但是,如果您是本地管理員,您仍可以使用 ODBC 數據來源管理員啟用計算機範圍的跟蹤。  
  
 要設定 ODBC 追蹤模式:  
  
1.  如有必要,請使用本地管理員組中具有成員資格的帳戶登錄。  
  
2.  從管理工具中,打開 ODBC 數據來源管理員。  
  
3.  按下 **「追蹤」** 選項卡。  
  
4.  使用機器**範圍追蹤「設定追蹤模式,以檢查所有使用者身份**複選框:  
  
5.  要啟用機器範圍的跟蹤,請選擇該複選框。  
  
6.  要返回到每個使用者跟蹤,請清除該複選框。  
  
7.  按一下 [套用]****。  
  
> [!NOTE]  
>  如果已在一種模式下開始跟蹤,則必須停止跟蹤並切換到其他模式才能成功更改模式。  
  
> [!IMPORTANT]  
>  僅當需要時才應啟用機器範圍的跟蹤;否則,它應該關閉。  
  
## <a name="visual-studio-analyzer-tracing"></a>視覺化工作室分析器追蹤  
  
> [!IMPORTANT]  
>  從 Windows 8 開始刪除了對可視化工作室分析器的支援(視覺工作室分析器僅包含在舊版本的 Visual Studio 中)。 對於其他故障排除機制,請使用 BID 跟蹤。  
  
 可視化 Studio®分析器追蹤提供有關 ODBC 層的性能和調試資訊。 所有傳出事件都將在頂級介面觸發,以盡可能準確地顯示 ODBC 元件所花費的時間。 可視化工作室分析器跟蹤需要設置源時註冊任何事件源。 有關此類跟蹤的詳細資訊,請參閱 Visual Studio 文件。

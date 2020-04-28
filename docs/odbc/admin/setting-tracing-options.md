---
title: 設定追蹤選項 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307191"
---
# <a name="setting-tracing-options"></a>設定追蹤選項
[ **Odbc 資料來源管理員**] 對話方塊的 [**追蹤**] 索引標籤可讓您設定追蹤 ODBC 函式呼叫的方式。  
  
## <a name="how-tracing-works"></a>追蹤的運作方式  
 當您從 [**追蹤**] 索引標籤啟動追蹤時，驅動程式管理員會記錄所有後續執行之應用程式的所有 ODBC 函數呼叫。 不會記錄在啟動追蹤之前執行之應用程式的 ODBC 函數呼叫。 ODBC 函式呼叫會記錄在您指定的記錄檔中。  
  
 只有在您按一下 [**立即停止追蹤**] 之後，才會停止追蹤。 請記住，追蹤作業開啟時，記錄檔會繼續增加，這會影響所有 ODBC 應用程式的效能。  
  
 如需追蹤的詳細資訊，請參閱[追蹤](../../odbc/reference/develop-app/tracing.md)。  
  
### <a name="changes-in-odbc-tracing"></a>ODBC 追蹤的變更  
 在 MDAC 2.7 SP2 之前，只允許在機器範圍內進行 ODBC 追蹤，其中追蹤會針對在任何身分識別下執行的所有 ODBC 應用程式，捕捉公開詳細資料。 這包括對 ODBC 相關活動的追蹤，可能會在代表其他本機使用者帳戶或內建安全性主體（如本機服務和網路服務）建立或執行的進程中發生。  
  
 根據預設，ODBC 追蹤現在會使用每個使用者模式。 不過，如果您是本機系統管理員，您仍然可以使用「ODBC 資料來源管理員」來啟用整部電腦的追蹤。  
  
 若要設定 ODBC 追蹤模式：  
  
1.  如有需要，請使用具有本機系統管理員群組成員資格的帳戶進行登入。  
  
2.  在 [系統管理工具] 中，開啟 [ODBC 資料來源管理員]。  
  
3.  按一下 [**追蹤**] 索引標籤。  
  
4.  使用 [所有使用者身分識別的**全機器追蹤**] 核取方塊來設定追蹤模式：  
  
5.  若要啟用整部電腦的追蹤，請選取核取方塊。  
  
6.  若要返回每個使用者的追蹤，請清除此核取方塊。  
  
7.  按一下 [套用]  。  
  
> [!NOTE]  
>  如果您已經在一種模式下啟動追蹤，就必須停止追蹤並切換至另一種模式，才能成功變更模式。  
  
> [!IMPORTANT]  
>  只有在需要時，才應該啟用整部電腦的追蹤;否則，應該保持關閉狀態。  
  
## <a name="visual-studio-analyzer-tracing"></a>Visual Studio Analyzer 追蹤  
  
> [!IMPORTANT]  
>  從 Windows 8 開始已移除 Visual Studio Analyzer 的支援（Visual Studio Analyzer 僅包含在舊版的 Visual Studio 中）。 如需替代的疑難排解機制，請使用出價追蹤。  
  
 Visual Studio®分析器追蹤提供有關 ODBC 層的效能和偵錯工具資訊。 所有傳出事件將會在最上層介面引發，以盡可能精確地呈現有關 ODBC 元件所花費時間的圖片。 Visual Studio Analyzer 追蹤需要在設定來源時註冊任何事件來源。 如需這種追蹤的詳細資訊，請參閱 Visual Studio 檔。

---
title: "設定追蹤選項 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: admin
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Visual Studio Analyzer tracing [ODBC]
- ODBC data source administrator [ODBC], tracing options
- tracing options [ODBC], ODBC data source administrator
ms.assetid: 44404a79-b716-4bc1-9ffb-70cd8239d237
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b1a62a03d3bb9e9876ed152bb4ac2cb8fb56ce66
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="setting-tracing-options"></a>設定追蹤選項
**追蹤** 索引標籤**ODBC 資料來源管理員** 對話方塊可讓您設定追蹤 ODBC 函數呼叫的方法。  
  
## <a name="how-tracing-works"></a>追蹤的運作方式  
 當您啟動追蹤從**追蹤**索引標籤上，驅動程式管理員會記錄所有 ODBC 函數呼叫的所有後續執行的應用程式。 不會記錄啟動追蹤之前執行的應用程式從 ODBC 函數呼叫。 ODBC 函數呼叫會在您指定的記錄檔記錄。  
  
 追蹤會停止，您必須按一下**追蹤立即停止**。 請記住，在追蹤時，記錄檔持續增加，而且這會影響所有的 ODBC 應用程式的效能。  
  
 如需有關追蹤的詳細資訊，請參閱[追蹤](../../odbc/reference/develop-app/tracing.md)。  
  
### <a name="changes-in-odbc-tracing"></a>ODBC 追蹤中的變更  
 MDAC 2.7 SP2 之前, ODBC 追蹤已只能進行全機器為基礎，追蹤會擷取有關所有 ODBC 應用程式的所有識別下執行的公開詳細資料。 這包括可能發生的處理程序建立或執行其他本機使用者帳戶和本機服務和網路服務等的內建安全性主體代表 ODBC 相關活動的追蹤。  
  
 根據預設，ODBC 追蹤現在會使用每個使用者模式。 如果您是本機系統管理員，不過，您可以仍然啟用全機器追蹤使用 ODBC 資料來源管理員。  
  
 若要設定 ODBC 追蹤模式：  
  
1.  如果有必要，使用登入具有本機系統管理員群組成員資格的帳戶。  
  
2.  從 [系統管理工具] 開啟 ODBC 資料來源管理員。  
  
3.  按一下**追蹤** 索引標籤。  
  
4.  設定追蹤模式使用**全機器追蹤所有的使用者身分的**核取方塊：  
  
5.  若要啟用全機器追蹤，請選取此核取方塊。  
  
6.  若要返回每個使用者追蹤，請清除核取方塊。  
  
7.  按一下 **[套用]**。  
  
> [!NOTE]  
>  如果您已經有一種模式中啟動追蹤，您必須停止追蹤並切換到其他模式的模式，以便順利變更。  
  
> [!IMPORTANT]  
>  全機器追蹤，才應該啟用時需要它。否則，它應該保持關閉狀態。  
  
## <a name="visual-studio-analyzer-tracing"></a>Visual Studio Analyzer 追蹤  
  
> [!IMPORTANT]  
>  Visual Studio Analyzer 的支援已移除開頭 （Visual Studio Analyzer 只包含在舊版的 Visual Studio）。 Windows 8 中。 如需疑難排解機制的替代方法，使用 BID 追蹤。  
  
 Visual Studio® 分析器追蹤會提供效能和 ODBC 層的偵錯資訊。 所有傳出事件將引發在最上層的介面，以呈現為精確圖片儘可能花費在 ODBC 元件有關的時間。 Visual Studio Analyzer 追蹤需要註冊設定來源時的任何事件來源。 如需有關這種追蹤的詳細資訊，請參閱 Visual Studio 文件。

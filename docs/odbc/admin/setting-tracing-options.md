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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 13e8caf9f3a9643f8063d6227258245a603f1665
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67901628"
---
# <a name="setting-tracing-options"></a>設定追蹤選項
**追蹤**索引標籤**ODBC 資料來源管理員**對話方塊可讓您設定 ODBC 函數呼叫追蹤的方式。  
  
## <a name="how-tracing-works"></a>追蹤的運作方式  
 當您啟動追蹤，從**追蹤**驅動程式管理員 索引標籤，將會記錄所有的 ODBC 函數呼叫，用於所有後續執行的應用程式。 不會記錄啟動追蹤之前執行的應用程式從 ODBC 函數呼叫。 ODBC 函式呼叫會在您指定的記錄檔記錄。  
  
 追蹤會停止，在您按一下之後才**停止追蹤現在**。 請記住，在追蹤時，記錄檔會持續增加，而這會影響所有的 ODBC 應用程式的效能。  
  
 如需有關追蹤的詳細資訊，請參閱 <<c0> [ 追蹤](../../odbc/reference/develop-app/tracing.md)。  
  
### <a name="changes-in-odbc-tracing"></a>在 ODBC 追蹤變更  
 MDAC 2.7 在 SP2 之前，ODBC 追蹤只允許發生全機器為基礎，追蹤會擷取有關所有任何身分識別下執行的 ODBC 應用程式的公開詳細資料。 這包含 ODBC 相關的活動可能發生的處理程序建立或執行代表其他本機使用者帳戶和本機服務和網路服務等的內建安全性主體的追蹤。  
  
 根據預設，ODBC 追蹤現在會使用每個使用者模式。 如果您是本機系統管理員，不過，您可以仍然啟用全機器追蹤使用 ODBC 資料來源管理員。  
  
 若要設定 ODBC 追蹤模式：  
  
1.  如果有必要，使用登入具有本機系統管理員群組成員資格帳戶。  
  
2.  從 系統管理工具 開啟 ODBC 資料來源管理員。  
  
3.  按一下 [**追蹤**] 索引標籤。  
  
4.  設定 追蹤使用模式**所有的使用者身分識別的全機器追蹤**核取方塊：  
  
5.  若要啟用全機器追蹤，請選取核取方塊。  
  
6.  若要傳回以每位使用者進行追蹤，請清除核取方塊。  
  
7.  按一下 **[套用]** 。  
  
> [!NOTE]  
>  如果您已有一種模式中啟動追蹤，您必須停止追蹤，並切換至 已成功變更模式的其他模式。  
  
> [!IMPORTANT]  
>  需要; 時，應該只啟用全機器追蹤否則，它應該保持關閉狀態。  
  
## <a name="visual-studio-analyzer-tracing"></a>Visual Studio Analyzer 追蹤  
  
> [!IMPORTANT]  
>  從 Windows 8 （Visual Studio Analyzer 只包含在舊版的 Visual Studio 中）。 開始，已移除 Visual Studio analyzer 的支援。 如需疑難排解機制的替代方法，使用 BID 追蹤。  
  
 Visual Studio® 分析器追蹤會提供效能和 ODBC 層級的偵錯資訊。 所有傳出事件會在最上層的介面，以呈現為精確圖片以最相關的時間花費在 ODBC 元件中引發。 Visual Studio Analyzer 追蹤需要註冊時的來源設定的任何事件來源。 如需有關這種追蹤的詳細資訊，請參閱 Visual Studio 文件。

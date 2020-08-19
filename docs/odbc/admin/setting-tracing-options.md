---
description: 設定追蹤選項
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
ms.openlocfilehash: 72e3805eded00b1bfa0c984d5ff0ace1ae1494fc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476950"
---
# <a name="setting-tracing-options"></a>設定追蹤選項
[ **Odbc 資料來源管理員**] 對話方塊的 [**追蹤**] 索引標籤可讓您設定追蹤 ODBC 函數呼叫的方式。  
  
## <a name="how-tracing-works"></a>追蹤的運作方式  
 當您從 [ **追蹤** ] 索引標籤啟動追蹤時，驅動程式管理員會針對所有後續執行的應用程式，記錄所有 ODBC 函式呼叫。 不會記錄在啟動追蹤之前執行的應用程式的 ODBC 函式呼叫。 ODBC 函式呼叫會記錄在您指定的記錄檔中。  
  
 只有在您按一下 [ **立即停止追蹤**] 之後，才會停止追蹤。 請記住，當追蹤開啟時，記錄檔會持續增加，而且會影響所有 ODBC 應用程式的效能。  
  
 如需追蹤的詳細資訊，請參閱 [追蹤](../../odbc/reference/develop-app/tracing.md)。  
  
### <a name="changes-in-odbc-tracing"></a>ODBC 追蹤的變更  
 在 MDAC 2.7 SP2 之前，只允許在整個電腦上進行 ODBC 追蹤，而追蹤會捕捉在任何身分識別下執行的所有 ODBC 應用程式的相關詳細資料。 這包括對 ODBC 相關活動的追蹤，這些活動可能會代表其他本機使用者帳戶和內建安全性主體（例如本機服務和網路服務）所建立或執行的進程。  
  
 根據預設，ODBC 追蹤現在會使用每一使用者模式。 但是，如果您是本機系統管理員，您仍然可以使用「ODBC 資料來源管理員」來啟用整台電腦的追蹤。  
  
 若要設定 ODBC 追蹤模式：  
  
1.  如有必要，請使用具有本機系統管理員群組成員資格的帳戶登入。  
  
2.  在 [系統管理工具] 中，開啟 [ODBC 資料來源管理員]。  
  
3.  按一下 [追蹤] 索引標籤。  
  
4.  使用 [所有使用者身分識別的 **全機器追蹤** ] 核取方塊來設定追蹤模式：  
  
5.  若要啟用整台電腦的追蹤，請選取核取方塊。  
  
6.  若要返回每一使用者追蹤，請清除核取方塊。  
  
7.  按一下 [套用]。  
  
> [!NOTE]  
>  如果您已經在單一模式中啟動追蹤，則必須停止追蹤並切換至另一種模式，才能成功變更模式。  
  
> [!IMPORTANT]  
>  您應該只在需要時啟用電腦範圍的追蹤;否則應該保持關閉狀態。  
  
## <a name="visual-studio-analyzer-tracing"></a>Visual Studio Analyzer 追蹤  
  
> [!IMPORTANT]  
>  從 Windows 8 開始，Visual Studio Analyzer 的支援已移除 (Visual Studio Analyzer 僅包含在舊版的 Visual Studio ) 中。 如需替代的疑難排解機制，請使用「投標追蹤」。  
  
 Visual Studio®分析器追蹤會提供有關 ODBC 層的效能和偵錯工具資訊。 所有外寄事件將會在最上層介面引發，以盡可能以 ODBC 元件所花費的時間呈現正確的圖片。 Visual Studio Analyzer 追蹤需要在設定來源時註冊任何事件來源。 如需這種追蹤的詳細資訊，請參閱 Visual Studio 檔。

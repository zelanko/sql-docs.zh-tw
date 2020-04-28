---
title: 為什麼建立 ODBC？ | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], about ODBC
ms.assetid: ba6eb993-316b-4650-bab8-d76583c00e53
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 22173b0ad3dd8abf2d168b41a16a03bc414022ce
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302779"
---
# <a name="why-was-odbc-created"></a>為什麼建立 ODBC？
在過去，公司使用了單一 DBMS。 所有資料庫存取都是透過該系統的前端來完成，或透過撰寫成以獨佔方式使用該系統的應用程式來進行。 不過，隨著電腦的使用成長，還有更多電腦硬體和軟體變得可用，公司也開始取得不同的 Dbms。 原因很多：人們購買了什麼是最便宜的、什麼是最快的、哪些是最新的，也就是市場上最新的資訊，以及最適合單一應用程式的工作。 其他原因是重組和合併，其中先前具有單一 DBMS 的部門現在有數個。  
  
 隨著個人電腦的出現，問題的成長也更複雜。 這些電腦引進了一系列的工具，用來查詢、分析和顯示資料，以及一些價格實惠、便於使用的資料庫。 從一開始，單一的公司通常會將資料散佈在各式各樣的桌上型電腦、伺服器和 minicomputers 中，儲存在各種不相容的資料庫中，並由大量不同的工具存取，其中少數人都可以取得所有資料。  
  
 最後一項挑戰就是用戶端/伺服器運算的問世，它會尋求最有效率的電腦資源使用方式。 價格實惠的個人電腦（用戶端）位於桌面上，並提供資料的圖形前端和一些成本實惠的工具，例如試算表、圖表程式和報表產生器。 Minicomputers 和大型電腦（伺服器）會裝載 Dbms，讓他們可以使用其運算能力和中央位置來提供快速、協調的資料存取。 那麼，要如何將前端軟體連線到後端資料庫呢？  
  
 獨立軟體廠商（Isv）面臨類似的問題。 撰寫 minicomputers 和大型主機資料庫軟體的廠商，通常會被迫為每個 DBMS 撰寫一個應用程式版本，或為他們想要存取的每個 DBMS 撰寫 DBMS 專屬的程式碼。 撰寫個人電腦軟體的廠商必須為每個想要使用的不同 DBMS 撰寫資料存取常式。 這通常表示耗用大量資源來撰寫和維護資料存取常式，而不是應用程式，而且應用程式通常不會在其品質上銷售，而是可以存取指定 DBMS 中的資料。  
  
 這兩組開發人員都是存取不同 Dbms 中資料的方法。 大型主機和 minicomputer 群組需要一種方法，在單一應用程式中合併來自不同 Dbms 的資料，而個人電腦群組則需要這項功能，以及撰寫與任何一個 DBMS 無關的單一應用程式。 簡言之，這兩個群組都需要互通的方式來存取資料;它們需要開放式資料庫連接。

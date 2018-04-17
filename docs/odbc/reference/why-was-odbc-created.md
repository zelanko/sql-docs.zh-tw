---
title: 為什麼建立 ODBC？ | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ODBC [ODBC], about ODBC
ms.assetid: ba6eb993-316b-4650-bab8-d76583c00e53
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 82e2bd742d4736e75e5bfa3d6437304a32b289ed
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="why-was-odbc-created"></a>為什麼建立 ODBC？
在過去，公司會使用單一的 DBMS。 透過該系統的前端或以獨佔方式使用該系統撰寫的應用程式，已完成所有的資料庫存取權。 不過，使用電腦成長及更多的電腦硬體和軟體變成可用時，公司啟動，以取得不同的 Dbms。 原因是許多： 人購買為何便宜，是最快，其功能已知道，是最新市場，最適合處理單一應用程式上。 因為其他原因而進行重組及合併的關係，其中先前單一 DBMS 部門現在有數個。  
  
 問題成長的個人電腦提供了更複雜。 在主機中的查詢、 分析及顯示資料，以及許多便宜，方便使用的資料庫的工具帶這些電腦。 從那時起，單一公司通常具有散佈在各種桌面、 伺服器和結果，儲存在各種不同的不相容的資料庫，而存取不同的工具，其中少無法到達的所有資料的大量資料。  
  
 最終的挑戰隨附的用戶端/伺服器電腦中，它會尋找以最有效率地使用電腦資源。 低成本的個人電腦 （用戶端） 放在桌面上，並提供這兩個圖形化前端資料的數量和低成本的工具，例如試算表、 圖表程式和報表產生器。 結果和大型主機電腦 （伺服器） 主控的 Dbms，其中可以使用其運算能力和中央位置來提供快速、 一致的資料存取。 如何再已連線到後端資料庫的前端軟體？  
  
 類似的問題會面臨獨立軟體廠商 (Isv)。 寫入結果和大型主機資料庫軟體的供應商通常已強制為每個 DBMS 撰寫一個版本的應用程式，或為他們想要存取每個 DBMS 撰寫 DBMS 專屬的程式碼。 供應商撰寫的個人電腦的軟體必須為每個與他們想要使用的不同 DBMS 撰寫資料存取常式。 這通常意味著大量的資源已花費撰寫及維護資料存取常式，而不是應用程式，並不是在品質上，但無法存取指定的 DBMS 中的資料通常銷售應用程式。  
  
 兩邊的開發人員所需的不同 Dbms 中存取資料的方法。 大型主機及迷你電腦群組所需的方式合併在單一的應用程式中的不同 Dbms 的資料，而這項功能，以及撰寫獨立於任何一個 DBMS 的單一應用程式的方式，所需的個人電腦群組。 簡單地說，這兩個群組都需要可互通的方式存取資料;它們需要開放式資料庫連接。

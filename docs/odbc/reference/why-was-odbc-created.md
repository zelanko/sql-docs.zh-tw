---
description: 為什麼建立 ODBC？
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
ms.openlocfilehash: 6ce24a4856c3bae6d271712a948e1ae5e2ceecbf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428790"
---
# <a name="why-was-odbc-created"></a>為什麼建立 ODBC？
在過去，公司使用了單一 DBMS。 所有資料庫存取都是透過該系統的前端，或透過專門用來處理該系統的應用程式來完成。 不過，隨著電腦的使用成長及更多電腦硬體和軟體的使用，公司也開始取得不同的 Dbms。 原因有很多：人們購買了最便宜、哪些是最快的、他們已經知道的最新內容、市場上最新的功能，以及最適合單一應用程式的工作。 其他原因是重組和合併，而先前具有單一 DBMS 的部門有數個。  
  
 隨著個人電腦的出現，此問題的成長變得更複雜。 這些電腦引進了一系列的工具，可用來查詢、分析和顯示資料，以及一些便宜、容易使用的資料庫。 從那一開始，單一的公司通常會將資料分散在各式各樣的桌上型電腦、伺服器和 minicomputers 中，儲存在各種不相容的資料庫中，並透過大量的不同工具來存取，其中有些工具可能會取得所有資料。  
  
 最後一項挑戰是用戶端/伺服器運算的問世，它會搜尋最有效率的電腦資源使用。 便宜的個人電腦 () 位於桌面上的用戶端，並提供資料的圖形化前端和一些便宜的工具，例如試算表、圖表程式和報表產生器。 Minicomputers 和大型主機電腦 (伺服器) 裝載 Dbms，讓他們可以使用其運算能力和集中位置來提供快速、協調的資料存取。 如何將前端軟體連線到後端資料庫？  
  
 與獨立軟體廠商 (Isv) 類似的問題。 針對 minicomputers 和大型主機撰寫資料庫軟體的廠商，通常會被迫為每個 DBMS 撰寫一個應用程式版本，或為他們想要存取的每個 DBMS 撰寫 DBMS 特定的程式碼。 撰寫個人電腦軟體的廠商必須為他們想要使用的每個不同 DBMS 撰寫資料存取常式。 這通常表示撰寫和維護資料存取常式（而不是應用程式）所花費的大量資源，而應用程式通常不會在其品質的情況下銷售，但它們是否可以存取指定 DBMS 中的資料。  
  
 這兩組開發人員都需要存取不同 Dbms 中的資料。 大型主機和 minicomputer 群組需要一種方式，在單一應用程式中合併來自不同 Dbms 的資料，而個人電腦群組則需要這項功能，以及撰寫與任何一個 DBMS 無關的單一應用程式。 簡單地說，這兩個群組需要可互通的方式來存取資料;他們需要開放式資料庫連接。

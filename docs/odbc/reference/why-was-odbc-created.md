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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8cfdd0babe84d309391b3e1ca546c4e05fdf1331
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68049173"
---
# <a name="why-was-odbc-created"></a>為什麼建立 ODBC？
在過去，公司會使用單一的 DBMS。 透過該系統的前端或撰寫以獨佔方式使用該系統的應用程式，已完成的所有資料庫存取。 不過，使用電腦成長及更多的電腦硬體與軟體成為可用時，公司已開始取得不同的 Dbms。 原因是許多項目：當時人們購買哪些項目為最便宜，是最快，他們已經知道，市場，成功的最佳單一應用程式是最新。 其他原因已重組和合併的關係，其中先前單一 DBMS 的部門現在有數個。  
  
 此問題已隨著個人電腦的更複雜。 在主應用程式的工具，如查詢、 分析及顯示資料，以及數個價格低廉、 簡單易用的資料庫回到這些電腦。 從那時起，單一公司通常會具有資料散布在大量的桌上型電腦、 伺服器和結果、 儲存在各種不同的不相容的資料庫，以及存取大量不同的工具，其中一些無法到達的所有資料。  
  
 最終的挑戰隨附用戶端/伺服器運算的問世的搜尋，以最有效率運用電腦資源。 低成本的個人電腦 （用戶端） 放在桌面上，並提供這兩個圖形化前端的資料以及低成本的工具，例如試算表、 圖表程式和報表產生器的數目。 結果和大型主機電腦 （伺服器） 裝載的 Dbms，其中可以使用其運算能力和中央位置來提供快速、 協調的資料存取。 如何再已連線到後端資料庫的前端軟體？  
  
 類似的問題會面臨獨立軟體廠商 (Isv)。 寫入結果和大型主機的資料庫軟體的供應商通常已強制為每個 DBMS 撰寫一個應用程式版本，或撰寫他們想要存取每個的 DBMS 的 DBMS 特定程式碼。 撰寫個人電腦的軟體供應商必須為每個與他們想要使用的不同 DBMS 撰寫資料存取常式。 這通常表示編寫及維護資料存取常式，而不是應用程式，並不能在其品質而無法存取指定的 DBMS 中的資料通常銷售應用程式花費大量的資源。  
  
 兩邊的開發人員所需的不同 Dbms 中存取資料的方式。 大型主機和迷你電腦群組需要方法來合併在單一應用程式中的不同 Dbms 的資料，而這項功能，以及撰寫獨立於任何一個的 DBMS 的單一應用程式的方式，所需的個人電腦群組。 簡單地說，這兩個群組所需的互通的方式來存取資料;他們需要開放式資料庫連接。

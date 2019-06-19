---
title: 如何：在 Transact-SQL 指令碼中概述及新增程式碼片段 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 543e7ce7-8639-4281-8a91-85314755e5de
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 842fb0e2b111b5bcd17b26d13db15e47aa5c1ad1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65099661"
---
# <a name="how-to-outline-and-add-snippets-to-transact-sql-script"></a>如何：在 Transact-SQL 指令碼中設定大綱及新增程式碼片段
SQL Server Data Tools 包含由程式碼片段組成的程式碼程式庫，這些程式碼片段已準備就緒可供您插入應用程式中。 每個程式碼片段都執行完整的指令碼工作，例如建立函式、資料表、觸發程序、索引、檢視、使用者定義資料類型等等。您只需要按幾下滑鼠，便能將程式碼片段插入原始程式碼。 這些程式碼片段因減少打字的時間而提升產能。  
  
需要瀏覽適當的程式碼片段時，您可以使用程式碼片段選擇器，從分類的程式碼片段清單中進行選擇。 在程式碼中加入程式碼片段後，可能有些部分需要自訂，例如以更適合的名稱取代變數名稱，或置入預存程序的實際邏輯。 您將發現為達到此目的，插入的程式碼片段在程式碼中有一個或多個以反白顯示的取代點。 如果您將滑鼠指標移到取代點上，就會顯示工具提示，說明如何變更程式碼。  
  
根據預設，所有的文字都顯示在 Transact\-SQL 編輯器中，但是您可以選擇在檢視中隱藏部分程式碼。 Transact\-SQL 編輯器能讓您選取程式碼區域，並將之設為可摺疊，使其出現在加號 (+) 之下。您可以按一下符號旁邊的加號 (+) 來展開或隱藏這個區域。 大綱的程式碼並未刪除，只是在檢視中隱藏起來。  
  
> [!WARNING]  
> 下列程序利用先前在[連接的資料庫開發](../ssdt/connected-database-development.md)和[專案導向的離線資料庫開發](../ssdt/project-oriented-offline-database-development.md)小節中的程序所建立的實體。  
  
### <a name="to-insert-snippets"></a>若要插入程式碼片段  
  
1.  以滑鼠右鍵按一下 [方案總管]  中的 [TradeDev]  專案，再依序選取 [加入]  和 [指令碼]  。 按一下 [加入新項目]  對話方塊中的 [加入]  。  
  
2.  以滑鼠右鍵按一下 Transact\-SQL 編輯器，再選取 [插入程式碼片段]  。 程式碼片段選擇器隨即出現。  
  
3.  按兩下程式碼片段選擇器中的 [資料表]  ，再按兩下 [建立資料表]  。  
  
4.  請注意，取代點以黃色反白顯示。 將滑鼠停留在 `Sample_Table` 上，資訊提示隨即顯示取代的說明。 按兩下 `Sample_Table`，並將它變更為 `Shipper2`。  
  
5.  使用 TAB 鍵移至下一個取代點，即 `column_1`。 將它重新命名為 `Id`。 按照相同的步驟，將 `column_2` 重新命名為 `name`，並將它的資料類型變更為 `nvarchar(128)` 而且允許 `NULL`。  
  
### <a name="to-outline-code"></a>若要設定程式碼的大綱  
  
1.  請注意 CREATE TABLE 陳述式旁邊的 **-** 號。 在指令碼中按一下區段旁邊的 **-** 號加以隱藏。  
  
2.  以滑鼠右鍵按一下 Transact\-SQL 編輯器，再依序選取 [大綱]  和 [取消大綱]  移除大綱資訊，而不會影響編輯器中的基礎程式碼。  
  
3.  若要再次啟動設定程式碼的大綱，以滑鼠右鍵按一下 Transact\-SQL 編輯器，再依序選取 [大綱]  和 [啟動自動大綱]  。 您還可以選取 [切換所有大綱]  切換展開/隱藏區段。  
  

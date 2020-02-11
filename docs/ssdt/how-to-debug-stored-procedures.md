---
title: 針對預存程序進行偵錯
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
f1_keywords:
- SQL.DATA.TOOLS.EXECUTESTOREDPROCEDURE.DIALOG
ms.assetid: e3c8707f-0f6b-4265-8a5a-81f079330b52
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: efd64369a6a8e666d67f2c277df62dc9af9c4e99
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "75241435"
---
# <a name="how-to-debug-stored-procedures"></a>如何：針對預存程序進行偵錯

Transact\-SQL 偵錯工具透過顯示 SQL 預存程序的 SQL 呼叫堆疊、區域變數和參數，讓您以互動方式針對預存程序進行偵錯。 就像在其他程式設計語言中偵錯一樣，您可以在針對 Transact\-SQL 指令碼進行偵錯時檢視及修改區域變數和參數、檢視全域變數，以及控制和管理中斷點。  
  
這個範例會示範如何建立 Transact\-SQL 預存程序並以逐步執行方式針對它進行偵錯。  
  
> [!WARNING]  
> 下列程序使用在[連接的資料庫開發](../ssdt/connected-database-development.md)和[專案導向的離線資料庫開發](../ssdt/project-oriented-offline-database-development.md)小節中的程序所建立的實體。  
  
### <a name="to-debug-stored-procedures"></a>若要偵錯預存程序  
  
1.  以滑鼠右鍵按一下 [方案總管]  中的 [TradeDev]  專案，再依序選取 [加入]  和 [預存程序]  。 將這個新的預存程序命名為 **AddProduct**，然後按一下 [加入]  。  
  
2.  將下列程式碼貼入預存程序。  
  
    ```  
    CREATE PROCEDURE [dbo].[AddProduct]  
    @id int,  
    @name nvarchar(128)  
    AS  
    INSERT INTO [dbo].[Product] (Id, Name) VALUES (@id, @name)  
    ```  
  
3.  按 F5 建置並部署專案。  
  
4.  在 SQL Server 物件總管中，以滑鼠右鍵按一下 [本機]  節點底下的 [TradeDev]  資料庫，再選取 [新增查詢]  。  
  
5.  將下列程式碼貼入查詢視窗。  
  
    ```  
    EXEC [dbo].[AddProduct] 50, N'Contoso';  
    GO  
    ```  
  
6.  按一下左方視窗邊界，將中斷點加入至 `EXEC` 陳述式。  
  
7.  在 Transact\-SQL 編輯器工具列上，按綠色箭頭按鈕的下拉箭頭，接著選取 [使用偵錯工具執行]  以在偵錯模式下執行查詢。  
  
8.  或者，您可以從 SQL Server 物件總管開始偵錯。 以滑鼠右鍵按一下 [AddProduct]  預存程序 (位於 [本機]   -> [TradeDev]  資料庫 -> [可程式性]   -> [預存程序]  底下)。 選取 [偵錯程序...]  。如果物件需要參數，便會出現 [偵錯程序]  對話方塊，內有每個參數各佔一列的表格。 資料表中的每列均有一欄參數名稱，以及一欄該參數的值。 請輸入每一個參數的值，然後按一下 [確定]。  
  
9. 確認 [區域變數]  視窗已開啟。 如果未開啟，請按一下 [偵錯]  功能表，然後依序選取 [視窗]  和 [區域變數]  。  
  
10. 按 F11 逐步執行查詢。 請注意，預存程序的參數及各自的值會顯示在 [區域變數]  視窗中。 或者，將滑鼠停留在 `INSERT` 子句的 `@name` 參數上，您也會看到指派給這個參數的 **Contoso** 值。  
  
11. 按一下文字方塊中的 [Contoso]  。 輸入 **Fabrikam** 並按 ENTER，變更偵錯時 `name` 變數的值。 您也可以在 [區域變數]  視窗中變更其值。 請注意，參數的值現在以紅色顯示，代表它已變更。  
  
12. 按 F10 不進入其餘的程式碼。  
  
13. 在 SQL Server 物件總管中，重新整理 [TradeDev]  資料庫節點，以便在 [Product]  資料表的資料檢視下查看新內容。  
  
14. 在 SQL Server 物件總管中的 [本機]  節點底下，找到 [TradeDev]  資料庫的 [Product]  資料表。  
  
15. 以滑鼠右鍵按一下 [Product]  資料表，再選取 [檢視資料]  。 請注意，新的資料列已經加入至資料表。  
  

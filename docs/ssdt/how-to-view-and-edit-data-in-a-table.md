---
title: 如何：檢視及編輯資料表中的資料 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- SQL.DATA.TOOLS.QUERYRESULTS.F1
- sql.data.tools.queryresults.executequerydeletingrow
ms.assetid: bb67ce83-a87a-4e14-84cd-9a5930fe74c8
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a52c3875e5b6368a8f5f229dd3309f60bd078fe7
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/17/2018
ms.locfileid: "39085330"
---
# <a name="how-to-view-and-edit-data-in-a-table"></a>如何：檢視及編輯資料表中的資料
您可以使用視覺化資料編輯器來檢視、編輯及刪除現有資料表的資料。  
  
> [!WARNING]  
> 下列程序將使用先前在[連接的資料庫開發](../ssdt/connected-database-development.md)小節的程序中所建立的實體。  
  
### <a name="to-edit-data-in-a-table-visually-using-the-data-editor"></a>若要使用資料編輯器，以視覺化方式編輯資料表  
  
1.  以滑鼠右鍵按一下 [SQL Server 物件總管] 中的 [Products] 資料表，再選取 [檢視資料]。  
  
2.  資料編輯器隨即啟動。 請注意，我們在先前的程序加入資料表中的資料列。  
  
3.  以滑鼠右鍵按一下 [SQL Server 物件總管] 中的 [Fruits] 資料表，再選取 [檢視資料]。  
  
4.  在資料編輯器中，分別為 [Id] 和 [Perishable] 輸入 **1** 和 **True**，然後按 ENTER 或 TAB 將焦點移離新資料列，以便加以認可到資料庫。  
  
5.  重複前面的步驟，將 **2**、**False** 和 **3**、**False** 輸入到資料表。  
  
    請注意，編輯資料列時按 ESC 即可將資料格的變更還原。  
  
6.  您可以按一下工具列上的 [指令碼] 按鈕，檢視編輯內容。 或者，您也可以使用 [編寫指令碼至檔案] 按鈕將編輯內容儲存到 .sql 指令碼檔案，等以後再執行。  
  
7.  以滑鼠右鍵按一下 [SQL Server 物件總管] 中的 [Trade] 資料庫，再選取 [新增查詢]。 在編輯器中，輸入 `select * from dbo.PerishableFruits`，然後按 [執行查詢] 按鈕傳回 `PerishableFruits` 檢視表所呈現的資料。  
  

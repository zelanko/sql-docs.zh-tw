---
title: "新增縮排 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-tutorial
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
ms.assetid: 9dce05c1-c52f-455d-8b8d-6f303e242760
caps.latest.revision: "25"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 5559f970627449d56863f4c9d933d5e6636f0bd2
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="lesson-2-2---adding-indentation"></a>課程 2-2 - 新增縮排
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] 查詢編輯器可讓您利用單一步驟來縮排一大段的程式碼，而且您也可以變更縮排的量。  
  
## <a name="indenting-code"></a>縮排程式碼  
  
#### <a name="to-indent-multiple-lines-of-code"></a>若要縮排多行程式碼  
  
1.  在工具列上，按一下 **[新增查詢]**。  
  
2.  建立第二項查詢，從 [Person] 結構描述的 [Person] 資料表中，選取 [BusinessEntityID]、[FirstName]、[MiddleName] 與 [LastName] 資料行。 請將每個資料行個別放在一行中，使程式碼看起來如下：  
  
    ```  
    -- Search for a contact  
    SELECT   
    BusinessEntityID,  
    FirstName,   
    MiddleName,   
    LastName  
    FROM Person.Person  
    WHERE LastName = 'Sanchez';  
    GO  
    ```  
  
3.  選取從 `BusinessEntityID` 到 `LastName` 的所有文字。  
  
4.  在 [SQL 編輯器] 工具列上，按一下 [增加縮排] 來同時縮排所有行。  
  
#### <a name="to-change-the-default-indentation"></a>若要變更預設縮排  
  
1.  在 **[工具]** 功能表上，按一下 **[選項]**。  
  
2.  依序展開 [文字編輯器] 和 [所有語言]，然後按一下 [索引標籤]，適當設定縮排的值。 請注意，您可以變更縮排大小，也可以變更 Tab 鍵距離，以及 Tab 鍵距離是否轉換成空格。  
  
    ![[定位點] 對話方塊的外觀](./media/lesson-2-2-adding-indentation/tabsdialog.gif "[定位點] 對話方塊的外觀")  
  
3.  按一下 [確定] 。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
[將查詢編輯器最大化](../../tools/sql-server-management-studio/lesson-2-3-maximizing-query-editor.md)  
  
  
  

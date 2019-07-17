---
title: 連接查詢編輯器 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 48725f54-a7b6-4b79-948e-965c1fe4eef1
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bcb2454d9f6b4a6df465c33ca218c4a960f8099b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "68187814"
---
# <a name="connecting-with-query-editor"></a>連接查詢編輯器
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 允許您在未連接伺服器的情況下，撰寫或編輯程式碼。 當伺服器無法使用，或您想節省寶貴的伺服器或網路資源時，這可能很有用。 您也可以在不開啟新 [查詢編輯器] 視窗或重新輸入程式碼的情況下，將查詢編輯器改成連接到新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。  
  
## <a name="coding-offline"></a>離線撰寫程式碼  
  
#### <a name="to-write-code-offline-and-then-connect-to-different-servers"></a>若要離線撰寫程式碼，然後連接到不同的伺服器  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 工具列上，按一下 [Database Engine 查詢]  來開啟 [查詢編輯器]。  
  
2.  在 [連接到 Database Engine]  對話方塊中，按一下 [取消]  。 此時會開啟查詢編輯器，查詢編輯器的標題列會指出您尚未連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。  
  
3.  在 [程式碼] 窗格中，輸入下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式：  
  
    ```  
    SELECT * FROM Production.Product;  
    GO  
    ```  
  
     此時您可以按一下 [連接]  、[執行]  、[剖析]  或 [顯示估計執行計畫]  來連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體，您可以從 [查詢]  功能表或 [查詢編輯器] 工具列來找到它們，也可以用滑鼠右鍵按一下 [查詢編輯器] 視窗，在捷徑功能表中找到它們。 在這個練習中，我們將使用工具列。  
  
4.  在工具列上，按一下 [執行]  按鈕來開啟 [連接到 Database Engine]  對話方塊。  
  
5.  在 [伺服器名稱]  文字方塊中，輸入您的伺服器名稱，然後按一下 [選項]  。  
  
6.  在 [連接屬性]  索引標籤的 [連接到資料庫]  清單中，瀏覽伺服器來選取 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]，然後按一下 [連接]  。  
  
7.  若要利用相同連接來開啟另一個 [查詢編輯器] 視窗，請在工具列上，按一下 [新增查詢]  。  
  
8.  若要變更連接，請以滑鼠右鍵按一下 [查詢編輯器] 視窗，指向 [連接]  ，然後按一下 [變更連接]  。  
  
9. 在 [連接到 SQL Server]  對話方塊中，如果有另一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，請選取它，然後按一下 [連接]  。  
  
 您可以利用查詢編輯器的這項新功能，輕易地在多部伺服器中執行相同的程式碼。 如果維護動作涉及多部類似的伺服器，這非常有用。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [加入縮排](lesson-2-2-adding-indentation.md)  
  
  

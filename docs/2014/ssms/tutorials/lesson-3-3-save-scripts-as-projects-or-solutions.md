---
title: 將指令碼儲存為專案或解決方案 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 72dfd37f-dbe7-4d1d-bda6-7eb54c7922d3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d64724108630e64ecfd654367180a6603aabe3e5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48125944"
---
# <a name="save-scripts-as-projects-or-solutions"></a>將指令碼儲存成專案或方案
  熟悉 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio 的開發人員會欣然接受 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的 [方案總管]。 支援您商務的指令碼可以分組成不同的指令碼專案，而且這些指令碼專案可以當作一個方案來一起管理。 當您將指令碼放在指令碼專案和方案中時，您可以將它們當作一個群組來一起開啟，也可以將它們一起儲存在 Visual SourceSafe 之類的原始檔控制產品中。 指令碼專案包括適當執行指令碼所需要的連接資訊，且可以包括支援文字檔之類的非指令碼檔案。  
  
 下列練習將建立一份簡短的指令碼來查詢放在指令碼專案和方案中的 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫。  
  
## <a name="using-script-projects-and-solutions"></a>使用指令碼專案和方案  
  
#### <a name="to-create-a-script-project-and-solution"></a>若要建立指令碼專案和方案  
  
1.  開啟 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]，再利用 [物件總管] 來連接伺服器。  
  
2.  在 **[檔案]** 功能表上，指向 **[開新檔案]**，然後按一下 **[專案]**。 此時會開啟 [新增專案] 對話方塊。  
  
3.  在 [名稱] 文字方塊中，輸入 **StatusCheck**，並在 [範本] 中按一下 [SQL Server 指令碼]，然後按一下 [確定] 來開啟新的方案和指令碼專案。  
  
4.  在方案總管中，以滑鼠右鍵按一下 [連接]，然後按一下 [新增連接]。 [連接到伺服器] 對話方塊隨即開啟。  
  
5.  在 [伺服器名稱] 清單方塊中，輸入您伺服器的名稱。  
  
6.  按一下 [選項]，然後按一下 [連接屬性] 索引標籤。  
  
7.  在 [連接到資料庫] 方塊中，瀏覽伺服器，並選取 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫，然後按一下 [連接]。 此時會將包括資料庫的連接資訊加入專案中。  
  
8.  如果 [屬性] 視窗沒有出現，請在 [方案總管] 中按一下新的連接，再按 F4 鍵。 此時會出現連接的屬性，且會顯示連接的相關資訊，其中包括 [初始資料庫] 是 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]。  
  
9. 在方案總管中，以滑鼠右鍵按一下連接，然後按一下 [新增查詢]。 此時會建立一個稱為 **SQLQuery1.sql** 的新查詢，這個查詢會連接到伺服器上的 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫，並新增至您的指令碼專案中。  
  
10. 在 [查詢編輯器] 中，輸入下列查詢來判斷多少工作訂單的到期日在工作訂單開始日期之前。 (您可以從 [教學課程] 視窗中複製和貼上程式碼)。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT COUNT(WorkOrderID)  
    FROM Production.WorkOrder  
    WHERE DueDate < StartDate;  
  
    ```  
  
    > [!NOTE]  
    >  如果您需要更多空間來輸入您的查詢，請按 SHIFT+ALT+ENTER 鍵，切換成全螢幕模式。  
  
11. 在方案總管中，以滑鼠右鍵按一下 [SQLQuery1]，然後按一下 [重新命名]。 輸入 **Check Workorders****.sql** 作為查詢的新名稱，再按 ENTER 鍵。  
  
12. 若要儲存您的方案和指令碼專案，請在 [檔案] 功能表上，按一下 [全部儲存]。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [摘要：方案和指令碼專案](lesson-3-4-summary-solutions-and-script-projects.md)  
  
  

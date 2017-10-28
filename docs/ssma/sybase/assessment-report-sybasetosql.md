---
title: "評估報表 (SybaseToSQL) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: af24f2c4-5e86-4135-a4f3-a24faaeeefe7
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 1a7de1095387d52d2d7675f1d8b04cc739121636
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="assessment-report-sybasetosql"></a>評估報表 (SybaseToSQL)
評估報表視窗中顯示的資料庫物件的轉換結果[!INCLUDE[tsql](../../includes/tsql_md.md)]語法，並且也可幫助您評估複雜度及成本的移轉專案。  
  
若要存取評估的報表，在來源中繼資料總管，轉換選取的物件上按一下滑鼠右鍵**資料庫**，然後選取**建立報表**。  
  
## <a name="options"></a>選項  
**轉換統計資料**  
顯示依陳述式類型的轉換統計資料。 這個窗格會顯示時，才是群組物件，例如結構描述，或沒有程式碼的物件已選取左窗格中。  
  
**物件類別**  
顯示依物件類型的轉換統計資料。 這個窗格會顯示時，才是群組物件，例如結構描述，或沒有程式碼的物件已選取左窗格中。  
  
**統計資料**  
顯示所選物件的轉換統計資料。 只有在左窗格中選取個別物件以程式碼時，此窗格是可見。 您可能必須展開 **統計資料**若要檢視此窗格。  
  
**來源巡覽**  
顯示所選物件的 ASE 程式碼，並反白顯示程式碼，未轉換成[!INCLUDE[tsql](../../includes/tsql_md.md)]。 只有在左窗格中選取個別物件以程式碼時，此窗格是可見。  
  
按一下以設定或清除書籤的行號。 使用窗格頂端的按鈕來瀏覽程式碼。  
  
**目標導覽**  
顯示產生的轉換[!INCLUDE[tsql](../../includes/tsql_md.md)]選取的物件，並不會被轉換的程式碼的錯誤訊息的程式碼。 只有在左窗格中選取個別物件以程式碼時，此窗格是可見。  
  
按一下以設定或清除書籤的行號。 使用窗格頂端的按鈕來瀏覽程式碼。  
  
**訊息窗格**  
顯示錯誤、 警告和資訊訊息建立評估報表時，所產生。 訊息會依數字分組。 若要檢視造成此錯誤的程式碼，請按一下**錯誤**，**警告**，或**資訊**，展開圖形的訊息、 分類，然後按一下 訊息。  
  


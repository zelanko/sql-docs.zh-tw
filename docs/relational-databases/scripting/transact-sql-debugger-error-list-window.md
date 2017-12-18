---
title: "錯誤清單視窗 (Management Studio) | Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: ssms
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: VS.ErrorList
dev_langs: TSQL
helpviewer_keywords:
- error list window
- SQL Server Management Studio [SQL Server], error list window
ms.assetid: fae6327d-e268-44ae-a474-4a8f8f843129
caps.latest.revision: "24"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 14041b10f1585f267d068b050c08fa38f7eea3f0
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="transact-sql-debugger---error-list-window"></a>Transact-SQL 偵錯工具 - 錯誤清單視窗
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [錯誤清單] 會顯示[!INCLUDE[ssDE](../../includes/ssde-md.md)]查詢編輯器中從 IntelliSense 程式碼產生的語法和語意錯誤。  
  
## <a name="features-of-the-error-list"></a>錯誤清單的功能  
 [錯誤清單] 提供了以下功能：  
  
-   當您編輯指令碼時，[錯誤清單] 會顯示 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器中由 IntelliSense 產生的錯誤和警告。  
  
-   您可以按兩下任何錯誤訊息項目，將焦點放在產生錯誤之指令碼檔案的索引標籤上，然後移動到錯誤的位置。  
  
-   您可以篩選您想要顯示的項目，以及每個項目所要顯示的資訊欄。  
  
-   當您修正錯誤之後，此錯誤項目就會從 [錯誤清單] 中移除。  
  
-   當您關閉 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼檔案的索引標籤時，該檔案的錯誤就會從 [錯誤清單] 中移除。  
  
## <a name="working-with-the-error-list"></a>使用錯誤清單  
 若要顯示 [錯誤清單]，請執行下列其中一項：  
  
-   在 [檢視] 功能表上，按一下 [錯誤清單]。  
  
-   輸入鍵盤快速鍵 CTRL+\\、CTRL+E。  
  
 在您開啟 [錯誤清單] 之後，您可以執行下列動作來自訂您的檢視：  
  
-   若要排序清單，請按一下任何資料行標頭。 若要以另一個資料行來重新排序，請按住 SHIFT 鍵，然後按一下另一個資料行標頭。  
  
-   若要選取哪些資料行要顯示和哪些要隱藏，請從捷徑功能表中選取 [顯示資料行]。  
  
-   若要變更已顯示之資料行的順序，請將任一資料行標頭拖曳到左邊或右邊。  
  
 [錯誤清單] 不會連結到有關特定錯誤的其他資訊。  
  
## <a name="transact-sql-errors-in-management-studio"></a>Management Studio 中的 Transact-SQL 錯誤  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 會在以下位置顯示 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼的錯誤：  
  
-   [錯誤清單] 包含 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 編輯器中 IntelliSense 所找到的所有語法和語意錯誤。 當您編輯 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼時，會動態更新這份錯誤清單。 此清單包含編輯器在每一個 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼中找到的所有錯誤。 編輯器在發現指令碼中的錯誤之後，不會停止剖析檔案。 在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 中，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 編輯器中的 IntelliSense 不會支援所有的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 語法元素。 [錯誤清單] 只包含 IntelliSense 支援之 [!INCLUDE[tsql](../../includes/tsql-md.md)] 語法中的錯誤。  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器視窗底端的 [訊息] 索引標籤會顯示當執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼時，[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 所傳回的所有錯誤和訊息。 此清單要等到您再次執行此指令碼之後，才會變更。 當 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 找到一或兩個編譯錯誤之後，就會停止剖析批次；因此，[訊息] 索引標籤可能不會列出指令碼中的所有錯誤。  
  
 有時錯誤會同時列在兩個位置。 例如，指令碼檔案可能會有一個語法錯誤列在 [錯誤清單] 中。 如果您在更正錯誤之前執行此指令碼，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 剖析器可以偵測到相同的狀況，並在 [訊息] 索引標籤上傳回此錯誤訊息的另一個複本。  
  
> [!NOTE]  
>  [錯誤清單] 只會顯示 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器中的錯誤，而不會顯示 MDX、DMX 或 XML/A 編輯器中的錯誤。 所有的 MDX、DMX 和 XML/A 錯誤都會顯示在這些編輯器的 [訊息] 索引標籤上。  
  
## <a name="uielement-list"></a>UIElement 清單  
 當 [錯誤清單] 開啟時，資訊會顯示在以下欄中：  
  
 **預設順序**  
 顯示指示項目產生順序的整數。  
  
 **描述**  
 顯示錯誤項目的文字。 冗長的描述會切換到下一行。  
  
 **檔案**  
 顯示產生錯誤的指令碼檔案名稱。  
  
 **線條**  
 顯示指示包含錯誤之程式碼行的整數。  
  
 **資料行**  
 顯示指示程式碼行中之錯誤位置的整數。  
  
 **專案**  
 顯示包含指令碼檔案的專案名稱。  
  
  

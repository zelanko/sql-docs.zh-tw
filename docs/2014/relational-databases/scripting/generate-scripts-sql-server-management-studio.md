---
title: 產生指令碼
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 9711c617-3c68-4e5a-aea3-befc64d51524
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d9f97b1682fa8a2e04b5f1afcc2a552a326a9e43
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "75242096"
---
# <a name="generate-scripts-sql-server-management-studio"></a>產生指令碼 (SQL Server Management Studio)
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 提供兩種產生 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼的機制。 您可以使用 [**產生和發佈腳本] Wizard**來建立多個物件的腳本。 您也可以使用**物件總管**中的 [編寫組件的指令碼為]  功能表，為個別物件或多個物件產生指令碼。  
  
1.  **選擇方法： [**  [產生和發佈腳本] Wizard](#GenPubScriptWiz)，[物件總管 [編寫腳本為] 功能表](#OEScriptAsMenu)  
  
2.  **若要使用腳本做為功能表：**[編寫單一物件的腳本](#ScriptSingleObject)、[使用物件總管編寫兩個](#ScriptTwoObjectsOE)物件的腳本、[使用物件總管詳細資料編寫兩個物件](#ScriptTwoObjectsOED)的腳本    
  
## <a name="before-you-begin"></a>開始之前  
 選擇最符合您需求的機制。  
  
###  <a name="GenPubScriptWiz"></a> [產生和發佈指令碼精靈]  
 使用 [產生和發佈指令碼精靈]  ，為多個物件建立 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼。 此精靈會產生資料庫中所有物件的指令碼，或是您所選取之物件子集的指令碼。 此精靈具有許多適用於指令碼的選項，例如是否要包含權限、定序及條件約束等。 如需有關使用此精靈的指示，請參閱 [產生和發佈指令碼精靈](generate-and-publish-scripts-wizard.md)。  
  
###  <a name="OEScriptAsMenu"></a> 物件總管的 [編寫組件的指令碼為] 功能表  
 您可以使用物件總管的 [編寫組件的指令碼為]**** 功能表，編寫單一物件、多個物件或單一物件之多個陳述式的指令碼。 您可以選擇數種指令碼的其中一種，例如建立、變更或卸除物件。 您可以將指令碼儲存到 [查詢編輯器] 視窗，或是儲存到檔案或剪貼簿。 指令碼是使用 Unicode 格式所建立。  
  
##  <a name="ScriptSingleObject"></a> 產生單一物件的指令碼  
 **編寫單一物件的指令碼**  
  
1.  在 [物件總管] 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的執行個體，然後展開該執行個體。  
  
2.  展開 [資料庫]  ，然後展開含有要編寫指令碼之物件的資料庫。  
  
3.  展開物件的類別目錄。 例如，展開 [資料表]  或 [檢視表]  節點。  
  
4.  以滑鼠右鍵按一下物件，然後指向 [產生 **物件類型> 的指令碼為]\<** ，例如指向 [產生資料表的指令碼為]  。  
  
5.  指向指令碼類型，例如 [CREATE 至]  或 [ALTER 至]  。  
  
6.  選取儲存指令碼的位置，例如 [新增查詢編輯器視窗]  或 [剪貼簿]  。  
  
##  <a name="ScriptTwoObjectsOE"></a>若要使用物件總管產生兩個物件的腳本  
 **使用物件總管編寫兩個物件的腳本**  
  
 有時候，您可能會希望指令碼有多個選項，例如先卸除程序，再建立程序，或先建立資料表，再變更資料表。 如果您需要建立一個參考不同類型之物件 (例如資料表、檢視表及預存程序) 的指令碼，也可以使用下列程序以產生多個物件的指令碼。  
  
1.  在 [物件總管] 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的執行個體，然後展開該執行個體。  
  
2.  展開 [資料庫]  ，然後展開含有要編寫指令碼之物件的資料庫。  
  
3.  以滑鼠右鍵按一下第一個要編寫指令碼的物件，並指向 [產生 **物件類型> 的指令碼為]\<**，然後在 [另存新檔]**** 選項中選擇 [新增查詢編輯器視窗]**** 作為輸出目的地。  
  
4.  導覽至您想要編寫指令碼的第二個物件。  
  
5.  以滑鼠右鍵按一下物件，並指向 [產生 **物件類型> 的指令碼為]\<**，然後在 [另存新檔]**** 選項中選擇 [剪貼簿]**** 作為輸出目的地。  
  
6.  在針對第一個物件開啟的 [查詢編輯器] 視窗中，從剪貼簿貼上第二個物件的指令碼。  
  
##  <a name="ScriptTwoObjectsOED"></a>若要使用物件總管詳細資料產生兩個物件的腳本  
 **使用物件總管詳細資料編寫兩個物件的腳本**  
  
 您可以使用 [物件總管詳細資料]**** 窗格，產生相同類別目錄之多個物件的指令碼。  
  
1.  在 [物件總管] 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的執行個體，然後展開該執行個體。  
  
2.  展開 [資料庫]  ，然後展開含有要編寫指令碼之物件的資料庫。  
  
3.  展開想要編寫指令碼之物件類型的類別目錄節點，例如 [資料表]  節點。  
  
4.  選取 **F7** 或是開啟 [檢視]  功能表並選取 [物件總管詳細資料]  ，開啟 [物件總管詳細資料]  窗格。  
  
5.  以滑鼠左鍵按一下您想要編寫指令碼的其中一個物件。  
  
6.  Crtl + 以滑鼠左鍵按一下您想要編寫指令碼的第二個物件。  
  
7.  以滑鼠右鍵按一下其中一個選取的物件，然後選取 [產生 **物件類型> 的指令碼為]\<** 。  
  
  

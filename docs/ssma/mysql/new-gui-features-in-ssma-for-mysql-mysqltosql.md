---
title: SSMA for MySQL (MySQLToSQL) 中的新 GUI 功能 |Microsoft 文件
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-mysql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 0e59e2dc-1e4a-47c0-a5c3-ae7b5f5e469c
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8ad56e3bb27184bd715e611ba61ad6c95e66037d
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2018
---
# <a name="new-gui-features-in-ssma-for-mysql-mysqltosql"></a>SSMA for MySQL (MySQLToSQL) 中的新 GUI 功能
本章節描述 SSMA 使用者介面的新功能  
  
## <a name="layouts"></a>版面配置  
這項功能可讓您選擇其中一個預先定義的兩個視窗配置，或建立您自己的配置。 若要存取版面配置 子功能表，請在 檢視 功能表上指向版面配置。 您那里選擇其中一個現有的配置、 加入目前的配置或管理配置。  
  
### <a name="add-current-layout"></a>新增目前的配置  
若要儲存目前的視窗配置，在 檢視 功能表上指向版面配置，然後按一下 加入目前的配置。  
  
### <a name="choose-predefined-layout"></a>選擇預先定義的配置  
若要選擇其中一個預先定義的配置，在 檢視 功能表上指向版面配置，，然後按一下 預設版面配置頁或不含總管。 您也可以使用快速鍵 Ctrl + Alt + 1 或 Ctrl + Alt + 2 的預先定義的配置分別。  
  
### <a name="choose-user-defined-layout"></a>選擇使用者定義的配置  
若要選擇使用者定義的配置，檢視 功能表上指向版面配置，再按一下其中一個使用者定義的配置。 您也可以使用定義在配置的捷徑。  
  
### <a name="manage-layouts"></a>管理配置  
若要開啟管理配置 對話方塊，檢視 功能表上指向 版面配置，然後按一下 管理配置。 管理配置對話方塊中您會發現現有配置的清單對話方塊的左側。 那里您可以選取要變更其設定的配置。 也可以變更清單中的配置順序或刪除使用按鈕在清單頂端的配置。 在對話方塊的右側，您可以變更下列版面配置設定：  
  
-   版面配置名稱  
  
-   同步處理的中繼資料瀏覽器  
  
-   可見性與來源和目標中繼資料瀏覽器的寬度  
  
-   來源或目標的 windows 和其大小的可見性  
  
-   可見性與輔助視窗的高度  
  
## <a name="bookmarks"></a>書籤  
這項功能可讓您設定在來源中的一個或多個書籤或目標程式碼，快速找到使用快速鍵的書籤、 管理與易記對話方塊書籤。  
  
### <a name="toggle-bookmark"></a>切換書籤  
您可以設定/移除書籤以下列方式：  
  
-   使用來源或目標 SQL 視窗頂端的按鈕切換書籤  
  
-   在 SQL 視窗左邊的灰色區域上按一下  
  
-   使用 Ctrl + Shift +&lt;0..9&gt;設定編號的書籤  
  
### <a name="bookmark-navigation"></a>書籤導覽  
您可以逐步解說的書籤，以下列方式：  
  
-   使用按鈕下一個書籤，SQL 視窗頂端的上一個書籤  
  
-   使用 Ctrl +&lt;0..9&gt;來尋找已編號的書籤  
  
-   使用按鈕移至或檢視原始檔中管理書籤對話方塊  
  
### <a name="removing-bookmark"></a>移除書籤  
您可以移除書籤，以下列方式：  
  
-   使用 SQL 視窗頂端的清除的按鈕來移除目前的文件中的所有書籤  
  
-   使用按鈕移除] 或 [全部移除中管理書籤對話方塊  
  
### <a name="manage-bookmarks"></a>管理書籤  
若要開啟管理書籤對話方塊中的，編輯 功能表上按一下 管理書籤。 在對話方塊中您會看到一份現有書籤。 您可以使用對話方塊右側的按鈕，來管理這些書籤。  
  
## <a name="object-history"></a>物件的歷程記錄  
GUI 物件記錄可讓您下列好處導覽物件時：  
  
-   您可以使用向前移及上一步 按鈕來瀏覽過的物件  
  
-   當您回到物件時，回已離開 [相同] 索引標籤  
  
-   當您回到物件和索引標籤是 SQL 時，回還剩下的相同資料指標位置  
  
## <a name="advanced-search-capabilities"></a>進階的搜尋功能  
進階的搜尋功能，會提供功能強大且靈活的搜尋功能，並讓您尋找物件宣告、 取得物件資訊、 執行快速搜尋、 執行進階搜尋中使用的模式等的類別目錄中的物件。  
  
### <a name="get-quick-information"></a>取得快速資訊  
您可以取得游標所在的位置，以下列方式在物件上的快速資訊：  
  
-   按一下 SQL 視窗頂端的按鈕快速諮詢  
  
-   以滑鼠右鍵按一下快顯功能表中選取 快速諮詢  
  
-   Press Ctrl+Shift+Space  
  
### <a name="find-declaration"></a>尋找宣告  
您可以移至的物件，在游標位置，以下列方式宣告：  
  
-   按一下 在 SQL 視窗頂端的按鈕移至宣告  
  
-   以滑鼠右鍵按一下快顯功能表中選取 移至宣告  
  
-   按下 f12 鍵  
  
### <a name="quick-search"></a>快速搜尋  
您可以執行快速的文字搜尋，使用下列功能：  
  
-   您可以開始使用 Ctrl + F 快速鍵搜尋  
  
-   您可以使用 F3 重複最後一個搜尋轉寄  
  
-   您可以使用 Shift + F3 重複最後一個搜尋的回溯  
  
-   您可以使用 Ctrl + F3，以尋找下一個出現的文字在游標位置  
  
-   您可以使用 Ctrl + Shift + F3 找到上一個出現的文字在游標位置  
  
-   您也可以執行所有這些動作的功能表項目。  
  
### <a name="advanced-search"></a>進階搜尋  
若要開啟進階搜尋] 對話方塊的 [編輯] 功能表點尋找，然後按一下 [進階搜尋。 在對話方塊中您可以尋找使用模式的任何物件。 您可以選擇在對話方塊頂端搜尋區域和物件的類別。  
  

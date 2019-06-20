---
title: SSMA for Oracle (OracleToSQL) 中的新 GUI 功能 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 62e2d30f-a73f-42d9-a6ab-3510a8198f4e
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: ee8637bb85c390378dc5c886165ddfa12950e03b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63209821"
---
# <a name="new-gui-features-in-ssma-for-oracle-oracletosql"></a>SSMA for Oracle (OracleToSQL) 中的新 GUI 功能
此章節會描述 SSMA 使用者介面的新功能。  
  
## <a name="layouts"></a>版面配置  
這項功能可讓您選擇其中一個預先定義的兩個視窗配置，或建立您自己的配置。 若要存取版面配置 子功能表，請在 檢視 功能表上指向版面配置。 那里，您可以選擇其中一個現有的版面配置，加入新的版面配置，或管理配置。  
  
### <a name="add-current-layout"></a>新增目前的版面配置  
若要儲存目前的視窗配置，檢視] 功能表上指向版面配置，然後按一下 [加入目前的配置。  
  
### <a name="choose-predefined-layout"></a>選擇預先定義的版面配置  
若要選擇其中一個預先定義的配置，檢視] 功能表上指向版面配置，然後按一下 [預設的版面配置] 或 [沒有總管。 您也可以使用快速鍵 Ctrl + Alt + 1 或 Ctrl + Alt + 2 的預先定義的配置。  
  
### <a name="choose-user-defined-layout"></a>選擇使用者定義的版面配置  
若要選擇使用者定義的版面配置，檢視] 功能表上指向 [版面配置，，然後按一下其中一個使用者定義的版面配置。 您也可以使用版面配置定義的快速鍵。  
  
### <a name="manage-layouts"></a>管理配置  
若要開啟 管理配置 對話方塊，檢視 功能表上指向 版面配置，然後按一下 管理配置。 在 [管理配置] 對話方塊中，您會找到一份現有的版面配置對話方塊的左側。 那里，您可以選取要變更其設定的配置。 也可以變更清單中的版面配置順序，或刪除配置使用清單頂端的按鈕。 在對話方塊的右邊，您可以變更下列版面配置設定：  
  
-   配置名稱  
  
-   同步處理的中繼資料瀏覽器  
  
-   可見性和一個來源和目標中繼資料的總管的寬度  
  
-   來源或目標的 windows 和其大小的可見性  
  
-   可見性和輔助 windows 的高度  
  
## <a name="bookmarks"></a>書籤  
這項功能可讓您設定在來源中的一或多個書籤或目標程式碼，快速找到使用快速鍵的書籤、 管理書籤的好記的對話方塊。  
  
### <a name="toggle-bookmark"></a>切換書籤  
您可以設定/移除書籤功能如下：  
  
-   使用來源或目標 SQL 視窗頂端的按鈕切換書籤  
  
-   按一下 [SQL] 視窗的左邊的灰色區域  
  
-   使用 Ctrl + Shift +&lt;0..9&gt;設定編號書籤  
  
### <a name="bookmark-navigation"></a>書籤導覽  
您可以逐步解說的書籤，以下列方式：  
  
-   使用按鈕下一個書籤，SQL 視窗頂端的上一個書籤  
  
-   使用 Ctrl +&lt;0..9&gt;來尋找已編號的書籤  
  
-   使用按鈕移至或檢視原始檔中管理書籤對話方塊  
  
### <a name="removing-bookmark"></a>移除書籤  
您可以透過下列方式來移除書籤：  
  
-   使用清除 SQL 視窗頂端的按鈕來移除目前的文件中的所有書籤  
  
-   使用管理書籤 對話方塊中的按鈕移除 或 全部移除  
  
### <a name="manage-bookmarks"></a>管理書籤  
若要開啟 管理書籤對話方塊中的，在 編輯 功能表上按一下 管理書籤。 在對話方塊中，您會看到一份現有的書籤。 您可以使用對話方塊右側的按鈕，來管理書籤。  
  
## <a name="object-history"></a>物件的歷程記錄  
GUI 物件記錄可讓您下列優點時瀏覽物件：  
  
-   您可以使用上一步] 和 [向前移的按鈕來瀏覽您已經瀏覽物件  
  
-   當您回到物件時，回還剩下 [相同] 索引標籤  
  
-   當您回到物件和索引標籤是 SQL 時，回到您剩餘的相同資料指標位置  
  
## <a name="advanced-search-capabilities"></a>進階的搜尋功能  
進階的搜尋功能提供功能強大且靈活的搜尋功能，而且可讓您尋找物件宣告、 取得物件資訊、 執行快速搜尋、 執行進階搜尋使用模式等的類別目錄中的物件。  
  
### <a name="get-quick-information"></a>取得快速的資訊  
您可以取得資料指標位置，以下列方式在物件上的快速資訊：  
  
-   按一下 SQL 視窗頂端的按鈕快速諮詢  
  
-   以滑鼠右鍵按一下快顯功能表中選取 快速諮詢  
  
-   按下 Ctrl + Shift + 空格鍵  
  
### <a name="find-declaration"></a>尋找宣告  
您可以前往上物件的資料指標位置，以下列方式宣告：  
  
-   按一下 在 SQL 視窗頂端的按鈕移至宣告  
  
-   以滑鼠右鍵按一下快顯功能表中選取 移至宣告  
  
-   按下 f12 鍵  
  
### <a name="quick-search"></a>快速搜尋  
您可以執行快速的文字搜尋，使用下列功能：  
  
-   您可以開始搜尋使用快速鍵 Ctrl + F  
  
-   您可以使用 F3 重複最後一個搜尋轉寄  
  
-   您可以使用 Shift + F3 重複最後一個搜尋，回溯  
  
-   您可以使用 Ctrl + F3 來尋找下一個出現在游標位置的文字  
  
-   您可以使用 Ctrl + Shift + F3，以便尋找前一個出現的游標位置的文字  
  
-   您也可以執行所有這些動作的功能表項目。  
  
### <a name="advanced-search"></a>進階搜尋  
若要開啟進階搜尋] 對話方塊的 [編輯] 功能表點尋找，然後按一下 [進階搜尋。 在對話方塊中您可以尋找使用模式的任何物件。 您可以選擇對話方塊頂端搜尋區域和物件的類別。  
  

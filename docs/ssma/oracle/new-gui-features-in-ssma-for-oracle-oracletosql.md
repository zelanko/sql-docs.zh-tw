---
title: SSMA for Oracle 的新 GUI 功能（OracleToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 62e2d30f-a73f-42d9-a6ab-3510a8198f4e
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 295372026ec0a1eed0abb4e62a10bc56fd279d56
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "76910211"
---
# <a name="new-gui-features-in-ssma-for-oracle-oracletosql"></a>SSMA for Oracle 的新 GUI 功能（OracleToSQL）
本章說明 SSMA 使用者介面的新功能。  
  
## <a name="layouts"></a>版面配置  
這項功能可讓您選擇兩個預先定義的 windows 配置之一，或建立您自己的版面配置。 若要存取配置子功能表，請在 [視圖] 功能表上指向 [版面配置]。 您可以選擇其中一個現有的配置、加入新的版面配置，或管理版面配置。  
  
### <a name="add-current-layout"></a>加入目前的版面配置  
若要儲存目前的 windows 配置，請在 [View] 功能表上指向 [配置]，然後按一下 [加入目前的配置]。  
  
### <a name="choose-predefined-layout"></a>選擇預先定義的版面配置  
若要選擇其中一個預先定義的配置，請在 [View] 功能表上指向 [配置]，然後按一下 [預設版面配置] 或 [沒有流覽]。 您也可以使用快速鍵 Ctrl + Alt + 1 或 Ctrl + Alt + 2 來進行預先定義的版面配置。  
  
### <a name="choose-user-defined-layout"></a>選擇使用者定義的版面配置  
若要選擇使用者定義的版面配置，請在 [View] 功能表上指向 [配置]，然後按一下其中一個使用者定義的版面配置。 您也可以使用為版面配置定義的快捷方式。  
  
### <a name="manage-layouts"></a>管理版面配置  
若要開啟 [管理配置] 對話方塊，請在 [視圖] 功能表上指向 [配置]，然後按一下 [管理配置] 在 [管理版面配置] 對話方塊中，您會在對話方塊的左側找到現有的版面配置清單。 您可以在這裡選取要變更其設定的版面配置。 此外，您也可以在清單中變更版面配置順序，或使用清單頂端的按鈕來刪除版面配置。 在對話方塊的右側，您可以變更下列版面配置設定：  
  
-   配置名稱  
  
-   中繼資料流覽的同步處理  
  
-   來源和目標中繼資料流覽的可見度和寬度  
  
-   來源或目標視窗及其大小的可見度  
  
-   次要視窗的可見度和高度  
  
## <a name="bookmarks"></a>書籤  
這項功能可讓您在來源或目的程式代碼中設定一或多個書簽，使用快捷方式快速找到書簽，並以易記的對話方塊管理書簽。  
  
### <a name="toggle-bookmark"></a>切換書簽  
您可以透過下列方式來設定/移除書簽：  
  
-   在來源或目標 SQL 視窗頂端使用按鈕切換書簽  
  
-   按一下 [SQL] 視窗左側的灰色區域  
  
-   使用 Ctrl + Shift +&lt;0. 9&gt;設定編號的書簽  
  
### <a name="bookmark-navigation"></a>書簽流覽  
您可以透過下列方式逐步完成書簽：  
  
-   在 SQL 視窗頂端使用 [下一個書簽] 和 [上一個書簽] 按鈕  
  
-   使用 Ctrl +&lt;0. 9&gt;來尋找編號的書簽  
  
-   使用按鈕移至或流覽 [管理書簽] 對話方塊中的來源  
  
### <a name="removing-bookmark"></a>正在移除書簽  
您可以透過下列方式移除書簽：  
  
-   使用 [SQL] 視窗頂端的 [取消] 按鈕，以移除目前檔中的所有書簽  
  
-   在 [管理書簽] 對話方塊中使用按鈕移除或移除所有  
  
### <a name="manage-bookmarks"></a>管理書簽  
若要開啟 [管理書簽] 對話方塊，請按一下 [編輯] 功能表上的 [管理書簽]。 在對話方塊中，您會看到現有書簽的清單。 您可以使用對話方塊右側的按鈕來管理書簽。  
  
## <a name="object-history"></a>物件歷程記錄  
GUI 物件歷程記錄可讓您在流覽物件時有下列優點：  
  
-   您可以使用 [返回] 和 [下一頁] 按鈕來流覽您已造訪的物件。  
  
-   當您回到物件時，您會回到已離開的相同索引標籤  
  
-   當您回到物件，且索引標籤為 SQL 時，您會回到您所剩下的相同資料指標位置  
  
## <a name="advanced-search-capabilities"></a>先進的搜尋功能  
先進的搜尋功能提供強大且彈性的搜尋功能，並可讓您尋找物件宣告、取得物件資訊、執行快速搜尋、使用模式在類別中執行 advanced 物件搜尋等。  
  
### <a name="get-quick-information"></a>取得快速資訊  
您可以透過下列方式，在游標位置取得物件的快速資訊：  
  
-   按一下 SQL 視窗頂端的 [快速諮詢] 按鈕  
  
-   在滑鼠右鍵快顯功能表中選取 [快速諮詢]  
  
-   按 Ctrl + Shift + 空格鍵  
  
### <a name="find-declaration"></a>尋找宣告  
您可以透過下列方式移至位於游標位置的物件宣告：  
  
-   在 SQL 視窗頂端，按一下 [移至宣告] 按鈕  
  
-   選取滑鼠右鍵快顯功能表中的 [移至宣告]  
  
-   按 F12 鍵  
  
### <a name="quick-search"></a>快速搜尋  
您可以使用下列功能來執行快速文字搜尋：  
  
-   您可以使用 Ctrl + F 快捷方式開始搜尋  
  
-   您可以使用 F3 來向前重複上一次搜尋  
  
-   您可以使用 Shift + F3 來向後重複上一次搜尋  
  
-   您可以使用 Ctrl + F3，在游標位置尋找下一個出現的單字  
  
-   您可以使用 Ctrl + Shift + F3，在游標位置找到先前出現的單字  
  
-   您也可以使用功能表項目來執行所有這些動作。  
  
### <a name="advanced-search"></a>進階搜尋  
若要開啟 [高級搜尋] 對話方塊，請在 [編輯] 功能表點 [尋找]，然後按一下 [高級搜尋]。 在對話方塊中，您將能夠使用 pattern 來尋找任何物件。 在對話方塊的頂端，您可以選擇 [搜尋區域] 和 [物件類別]。  
  

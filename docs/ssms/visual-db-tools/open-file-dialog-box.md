---
title: 開啟檔案對話方塊 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-visual-db
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- vs.openfile
- vs.openproject
ms.assetid: 3e01b9f5-2b0a-4fb3-9da8-984d27d17b8a
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 20f698a0f85f54a31b18f74ad364de1fc1dfb187
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "37997920"
---
# <a name="open-file-dialog-box"></a>開啟檔案對話方塊
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
使用 [開啟檔案] 對話方塊來開啟磁碟中的現有檔案。 您也可以使用這個對話方塊，以不同的語言編碼選項來開啟已開啟的檔案。  
  
若要存取這個對話方塊，請從 [檔案] 功能表選取 [開啟]，然後再選擇 [檔案]。 從其他元素 (例如 [外部工具] 對話方塊) 開啟檔案時，也會出現這個對話方塊。 從 [檔案] 功能表選取 [開啟]，然後選擇 [專案/方案] 以開啟相同的 [開啟專案] 對話方塊。  
  
> [!NOTE]  
> 在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] 中開啟專案或元件之前，請判斷其程式碼的可信度。 在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] 中開啟專案或元件的動作可能會在本機電腦的信任處理序中執行它的程式碼。  
  
## <a name="option"></a>選項  
**查詢**  
從這個下拉式功能表找出現有的專案資料夾。 從此清單中選取資料夾會在主窗格中顯示該資料夾的內容。  
  
## <a name="my-places-bar"></a>我的位置工作列  
**桌面**  
顯示位於桌面上的檔案和資料夾。  
  
**我的專案**  
顯示使用者 [專案] 資料夾中的檔案和資料夾。  
  
**我的電腦**  
顯示磁碟片、硬碟和光碟機的內容。  
  
## <a name="folder-list"></a>資料夾清單  
**檔案名稱**  
使用此選項來篩選所顯示的檔案和資料夾。 輸入要篩選的完整或部分檔案名稱。 您可以使用星號 (*) 作為萬用字元。  
  
**檔案類型**  
使用此選項即可針對特定的檔案類型，對查詢中選取之資料夾或目錄的內容進行篩選。  
  
**開啟檔案和編碼選項**  
若要使用 [開啟檔案] 對話方塊指定目標檔案的編輯器，請選取 [開啟] 按鈕右邊的小矩形，並選擇 [開啟檔案]。 必要時，也可指定開啟所選取檔案時所要套用的語言編碼結構描述。 若要這樣做，請選取清單中含有「使用編碼方式」的程式，並選擇 [開啟] 以顯示 [編碼] 對話方塊。 這個按鈕不一定都可以使用。  
  
## <a name="toolbar"></a>工具列  
**往回導覽**  
回到最近檢視過的資料夾、磁碟機或網際網路位置。  
  
**移到上一層**  
導覽樹狀結構至樹狀結構檢視中的下一個最高資料夾。  
  
**搜尋 Web**  
此按鈕無法使用。  
  
**刪除**  
從存放區中刪除選取的檔案或資料夾。  
  
**新增資料夾**  
顯示 [新增資料夾] 對話方塊。 使用這個選項，可在 [查詢] 下拉式清單方塊中所選取的資料夾之下建立新的子資料夾。  
  
## <a name="views"></a>檢視  
提供選項，以排列和檢視 [檢視] 下拉式清單方塊中所選取之項目的內容。  
  
**縮圖**  
在顯示窗格中顯示項目的縮圖。  
  
**並排顯示**  
以大型圖示顯示檔案和資料夾。  
  
**圖示**  
以小型圖示顯示檔案和資料夾。  
  
**清單**  
以清單格式顯示檔案和資料夾。  
  
**詳細資料**  
以清單格式顯示檔案和資料夾的名稱、大小、類型和前次修改日期。 若要依特定詳細資料進行排序，請按一下它的資料行標頭。  
  
**WebView**  
此命令無法使用。  
  
## <a name="tools"></a>工具  
選取要套用至內容窗格中所選取之項目的工具。  
  
**刪除**  
從儲存體中刪除選取的檔案或資料夾。  
  
**連線網路磁碟機**  
開啟 [連線網路磁碟機] 對話方塊。  
  

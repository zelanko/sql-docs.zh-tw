---
title: 轉換設定 (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f551cf6e-1575-4206-9cca-975b5b43a6b8
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: fee221caf91d5d70f291f9351d05a00352e7cc00
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2018
ms.locfileid: "52400042"
---
# <a name="conversion-settings-mysqltosql"></a>轉換設定 (MySQLToSQL)
**[設定]** 索引標籤可讓使用者設定節點層級設定。 [] 索引標籤會位於下列 Metabase 節點：  
  
-   資料庫節點  
  
-   函式類別  
  
-   函式節點  
  
-   資料表類別  
  
-   在資料表節點  
  
## <a name="specifications"></a>規格：  
**設定** 索引標籤中有兩個使用者的設定、 上來。:  
  
1.  函式轉換  
  
2.  轉換資料表  
  
這些設定可根據 Metabase 節點類型。 例如，函式轉換相關的設定將無法在資料表節點  
  
> [!NOTE]  
> -   使用者所做的變更會儲存在專案工作區中，為個別的喜好設定檔案。  
> -   此檔案的副檔名會是**ccprefs**。  
  
1.  **函式轉換設定：**  
  
    1.  此索引標籤包含 **'強制函式轉換'** 選項。 選項可能會有下列四個值之一：  
  
        -   根據專案設定 [繼承] 轉換  
  
        -   永遠將轉換成函式  
  
        -   永遠將轉換成程序  
  
        -   根據專案設定轉換  
  
    2.  根據設定，此函式會轉換函式或預存程序。  
  
    3.  使用者所做的設定會儲存在串聯的喜好設定檔案上按一下**套用** 按鈕。  
  
2.  **資料表 [轉換] 設定：**  
  
    1.  此索引標籤包含 **'隱藏 ROWID 輔助的資料行產生'** 選項。 選項可能會有下列四個值之一：  
  
        -   根據專案設定 [繼承] 轉換  
  
        -   是  
  
        -   否  
  
        -   根據專案設定轉換  
  
    2.  如果 **'Yes'**，這項設定會禁止 ROWID 輔助的資料行建立在目標資料表上建立。  
  
    3.  使用者所做的設定會儲存在串聯的喜好設定檔案，方法是按一下**套用** 按鈕。  
  
## <a name="see-also"></a>另請參閱  
[專案設定 （轉換） (MySQL to SQL)](https://msdn.microsoft.com/7ad5fe44-6445-4ba8-a457-5af792631f11)  
  

---
description: 轉換設定 (MySQLToSQL)
title: 轉換設定 (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f551cf6e-1575-4206-9cca-975b5b43a6b8
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 1652913173dcd7427515db8c74d15afc75077820
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2020
ms.locfileid: "91988634"
---
# <a name="conversion-settings-mysqltosql"></a>轉換設定 (MySQLToSQL)
[ **設定** ] 索引標籤可讓使用者設定節點層級設定。 此索引標籤將會出現在下列的元資料庫節點上：  
  
-   資料庫節點  
  
-   函數類別目錄  
  
-   Function 節點  
  
-   資料表類別目錄  
  
-   資料表節點  
  
## <a name="specifications"></a>規格：  
[ **設定** ] 索引標籤有兩個使用者設定： [視覺效果]。  
  
1.  函數轉換  
  
2.  資料表轉換  
  
這些設定會根據 [元資料庫] 節點的類型而提供。 例如，在資料表節點上，將無法使用函數轉換的相關設定  
  
> [!NOTE]  
> -   使用者所做的變更將會以個別的喜好設定檔，儲存在專案工作區中。  
> -   這個檔案的副檔名將會是 **ccprefs**。  
  
1.  **函數轉換設定：**  
  
    1.  此索引標籤包含 [強制函式 **轉換** ] 選項。 選項可以有下列四個值的其中一個：  
  
        -   根據專案設定進行轉換 [繼承]  
  
        -   一律轉換成函式  
  
        -   一律轉換成程式  
  
        -   根據專案設定進行轉換  
  
    2.  根據設定，函數會轉換成函式或預存程式。  
  
    3.  使用者所做的設定會 **在按一下 [** 套用] 按鈕時，儲存在串聯喜好設定檔案中。  
  
2.  **資料表轉換設定：**  
  
    1.  此索引標籤包含「 **隱藏 ROWID 輔助資料行產生** 」選項。 選項可以有下列四個值的其中一個：  
  
        -   根據專案設定進行轉換 [繼承]  
  
        -   是  
  
        -   否  
  
        -   根據專案設定進行轉換  
  
    2.  如果為 **[是]**，則此設定會禁止在目標資料表上建立 ROWID 輔助資料行。  
  
    3.  在 **按一下 [** 套用] 按鈕時，使用者所做的設定會儲存在串聯喜好設定檔案中。  
  
## <a name="see-also"></a>另請參閱  
[專案設定 (轉換)  (MySQL 轉換成 SQL) ](./project-settings-conversion-mysqltosql.md)  

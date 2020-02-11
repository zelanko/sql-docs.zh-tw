---
title: 轉換設定（MySQLToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f551cf6e-1575-4206-9cca-975b5b43a6b8
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: debdd549dc010f7be6b9d9b37a4caf649d4e106a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68103117"
---
# <a name="conversion-settings-mysqltosql"></a>轉換設定 (MySQLToSQL)
[**設定**] 索引標籤可讓使用者設定節點層級設定。 索引標籤會在下列的 [元資料庫] 節點中提供：  
  
-   資料庫節點  
  
-   函數類別  
  
-   函數節點  
  
-   資料表類別  
  
-   資料表節點  
  
## <a name="specifications"></a>規則  
[**設定**] 索引標籤有兩個使用者設定：視覺效果。  
  
1.  函數轉換  
  
2.  資料表轉換  
  
這些設定會根據 [元資料庫] 節點的類型提供。 例如，資料表節點上將無法使用函數轉換的相關設定  
  
> [!NOTE]  
> -   使用者所做的變更會以個別的喜好設定檔案的形式，儲存在 [專案] 工作區中。  
> -   這個檔案的副檔名將會是**ccprefs**。  
  
1.  **函數轉換設定：**  
  
    1.  此索引標籤包含 [**強制函數轉換**] 選項。 選項可以有下列四個值的其中一個：  
  
        -   根據專案設定轉換 [繼承]  
  
        -   一律轉換成函式  
  
        -   一律轉換成程式  
  
        -   根據專案設定進行轉換  
  
    2.  根據設定，函式會轉換成函數或預存程式。  
  
    3.  使用者所做的設定會**在按一下 [** 套用] 按鈕時，儲存在級聯的喜好設定檔案中。  
  
2.  **資料表轉換設定：**  
  
    1.  此索引標籤包含 [**隱藏 ROWID 輔助資料行產生**] 選項。 選項可以有下列四個值的其中一個：  
  
        -   根據專案設定轉換 [繼承]  
  
        -   是  
  
        -   否  
  
        -   根據專案設定進行轉換  
  
    2.  如果為 **[是]**，這項設定會禁止在目標資料表上建立 ROWID 輔助資料行。  
  
    3.  使用者所做的設定會**在按一下 [** 套用] 按鈕時，儲存在級聯的喜好設定檔案中。  
  
## <a name="see-also"></a>另請參閱  
[專案設定（轉換）（MySQL 到 SQL）](https://msdn.microsoft.com/7ad5fe44-6445-4ba8-a457-5af792631f11)  
  

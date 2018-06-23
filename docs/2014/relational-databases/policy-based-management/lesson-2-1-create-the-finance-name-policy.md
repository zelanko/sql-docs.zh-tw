---
title: 建立 Finance Name 原則 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 56b2c852-fd69-4cd2-9b5d-977467b94fd9
caps.latest.revision: 26
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 417bb9c891d4fec3393f94cf9ccbdda0bf9d4bbe
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36136836"
---
# <a name="create-the-finance-name-policy"></a>建立 Finance Name 原則
  在這項工作中，您將會建立名為 Finance 的資料庫，然後建立要求所有資料表都以字母 **fintbl** 為開頭的條件。 接著，您將會建立原則和原則類別目錄，以便針對 Finance 資料庫中的資料表強制執行命名標準。  
  
### <a name="to-create-the-finance-database"></a>建立 Finance 資料庫  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中，開啟查詢視窗並執行下列陳述式：  
  
    ```  
    CREATE DATABASE Finance ;  
    GO  
    ```  
  
2.  在物件總管中，按一下 [資料庫]，然後按下 F5 重新整理資料庫的清單。  
  
### <a name="to-create-the-finance-tables-condition"></a>建立 Finance Tables 條件  
  
1.  在物件總管中，依序展開 [管理] 和 [原則管理]，以滑鼠右鍵按一下 [條件]，然後按一下 [新增條件]。  
  
2.  在 [建立新條件] 對話方塊的 [名稱] 方塊中，輸入 **Finance Tables**。  
  
3.  在 [Facet] 清單中，選取 [多部分名稱]。  
  
4.  在 [運算式] 區域的 [欄位] 方塊中，選取 [@Name]。在 [運算子] 方塊中，選取 [Like]。然後，在 [值] 方塊中，輸入 **'fintbl%'**，強制所有資料表名稱都以字母 **fintbl** 為開頭。  
  
5.  在 [描述] 頁面上，輸入**財務資料表名稱的開頭必須是 fintbl**，然後按一下 [確定] 建立條件。  
  
### <a name="to-create-the-finance-name-policy"></a>建立 Finance Name 原則  
  
1.  在物件總管中，以滑鼠右鍵按一下 [原則]，然後按一下 [新增原則]。  
  
2.  在 [建立新原則] 對話方塊的 [名稱] 方塊中，輸入 **Finance Name**。  
  
3.  在 [檢查條件] 清單中，選取 [Finance Tables]。 這會位於 [多部分名稱] 區域中。  
  
4.  在 [針對] 區域中，您將會看見可套用此原則的資料庫物件清單。 選取 [每份資料表] 的核取方塊。  
  
5.  在 [每個資料庫] 區域中，展開 [全部]，然後按一下 [新增條件]。  
  
6.  在 [建立新條件] 對話方塊的 [名稱] 方塊中，輸入 **Finance Database**。  
  
7.  在 [運算式] 方塊中，完成要包含 **@Name = 'Finance'** 的運算式，然後按一下 [確定] 關閉條件頁面。  
  
    > [!NOTE]  
    >  您可能必須按下 TAB 鍵跳離 [值] 方塊，才能啟用 [確定] 按鈕。  
  
8.  在 [評估模式] 清單中，選取 [變更時: 避免]。 這樣就會透過在 Finance 資料庫上建立資料庫觸發程序，強制執行此原則。  
  
9. 選取 [已啟用] 清單 ([已啟用] 方塊不會套用至 [視需要] 原則)。  
  
10. 在 [伺服器限制] 清單中，選取 [無]。  
  
11. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-create-the-finance-policy-category"></a>建立 Finance 原則類別目錄  
  
1.  在物件總管中，展開 [管理]，以滑鼠右鍵按一下 [原則管理]，然後按一下 [管理類別目錄]。  
  
2.  在**管理原則類別目錄**對話方塊的 **名稱**，型別`Finance`的空白方塊中，然後取消核取**託管資料庫訂閱**。 [託管資料庫訂閱] 將會強制執行個體中的每一個資料庫訂閱屬於這個原則類別目錄的原則。 基於這個理由，只有 Finance 資料庫應該訂閱 Finance Name 原則。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [訂閱和檢查 Finance Name 原則](lesson-2-2-subscribe-to-and-check-the-finance-name-policy.md)  
  
  
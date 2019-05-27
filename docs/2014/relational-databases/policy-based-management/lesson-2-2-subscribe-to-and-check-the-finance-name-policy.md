---
title: 訂閱和檢查 Finance Name 原則 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 126b4c4c-2a1c-4701-a0ad-8de23fbd7306
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3bbf6c9640882ffca2bbdbf82b2ef2667c394096
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66090688"
---
# <a name="subscribe-to-and-check-the-finance-name-policy"></a>訂閱和檢查 Finance Name 原則
  在這項工作中，您會將 Finance 資料庫設定為訂閱 Finance 原則類別目錄。 然後，您將測試 Finance Name 原則。  
  
### <a name="to-subscribe-to-the-finance-policy-category"></a>訂閱 Finance 原則類別目錄  
  
1.  在 [物件總管] 中，展開**資料庫**，以滑鼠右鍵按一下`Finance`，指向**原則**，然後按一下**類別**。  
  
2.  選取 **已訂閱**核取方塊`Finance`類別目錄。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-test-the-enforcement-of-the-finance-name-policy"></a>測試 Finance Name 原則的強制執行  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中，開啟查詢視窗。 執行下列陳述式，以便嘗試建立違反 **Finance Name** 原則的資料表。 此資料表違反了原則，因為資料表名稱並未以字母 **fintbl**為開頭。  
  
    ```  
    USE Finance ;  
    GO  
    CREATE TABLE NewTable  
    (Col1 int) ;  
    GO  
  
    ```  
  
     請注意，這個原則會讓您無法建立資料表，並且傳回提供原則名稱的參考用訊息。  
  
2.  若要提供有效的名稱，請依照下列內容修改程式碼並再次執行陳述式。  
  
    ```  
    USE Finance ;  
    GO  
    CREATE TABLE fintblNewTable  
    (Col1 int) ;  
    GO  
  
    ```  
  
     這次就會建立資料表。  
  
### <a name="to-apply-the-policy-to-the-whole-server"></a>將原則套用至整個伺服器  
  
1.  目前，只有 Finance 資料庫訂閱 Finance 原則類別目錄。 在許多情況下，將原則類別目錄套用至整個伺服器是比較簡單的方式。 在物件總管中，展開 [管理]，以滑鼠右鍵按一下 [原則管理]，然後按一下 [管理類別目錄]。  
  
2.  在 [管理原則類別目錄] 對話方塊中，找出 Finance 類別目錄，然後針對 Finance 類別目錄選取 [託管資料庫訂閱] 核取方塊。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)] 此時，Finance 類別目錄會套用至所有資料庫，但是您已建立的條件會將 Finance Name 原則限制為 Finance 資料庫。 這點就說明了如何以將在許多伺服器上正確套用的方式，使用複雜的條件組合來建立原則的目標。  
  
## <a name="summary"></a>總結  
 這個教學課程已經示範了如何建立以原則為基礎的管理條件、原則和原則群組，以及如何套用篩選和檢查以原則為基礎的管理目標是否符合。  
  
## <a name="next"></a>下一個  
 本教學課程已完成。 若要返回開頭，請按一下[教學課程：使用原則式管理來管理伺服器](tutorial-administering-servers-by-using-policy-based-management.md)。  
  
 如需教學課程的清單，請參閱 < [SQL Server 2014 的教學課程](../../tutorials/tutorials-for-sql-server-2014.md)。  
  
## <a name="see-also"></a>另請參閱  
 [使用原則式管理來管理伺服器](administer-servers-by-using-policy-based-management.md)  
  
  

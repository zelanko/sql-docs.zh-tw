---
title: 步驟 4：新增一般檔案目的地 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: f4088de3-16d8-419c-96a1-a2cd005d0a5b
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2a29d4953919644100b5863c3f4766895ea356c5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48075578"
---
# <a name="step-4-adding-a-flat-file-destination"></a>步驟 4：加入一般檔案目的地
  [查閱貨幣索引鍵] 轉換的錯誤輸出，將使得查閱作業失敗的任何資料列重新導向至 [指令碼] 轉換。 為了加強所發生錯誤的相關資訊，[指令碼] 轉換執行一個取得錯誤描述的指令碼。  
  
 在這項工作中，您將失敗資料列的所有資訊儲存至分隔檔案中供以後處理。 若要儲存失敗的資料列，您必須為包含該錯誤資料的文字檔加入及設定一般檔案連接管理員和一般檔案目的地。 透過設定「一般檔案」目的地使用之「一般檔案」連接管理員上的屬性，您可以指定「一般檔案」目的地如何格式化並寫入文字檔。 如需詳細資訊，請參閱＜ [Flat File Connection Manager](connection-manager/file-connection-manager.md) ＞和＜ [Flat File Destination](data-flow/flat-file-destination.md)＞。  
  
### <a name="to-add-and-configure-a-flat-file-destination"></a>加入和設定一般檔案目的地  
  
1.  按一下 **[資料流程]** 索引標籤。  
  
2.  在 **[SSIS 工具箱]** 中，展開 **[其他]**，然後將 **[一般檔案目的地]** 拖曳至 [資料流程] 設計介面中。 將 **[一般檔案目的地]** 直接放在 **[取得錯誤描述]** 轉換之下。  
  
3.  按一下 [ **取得錯誤描述** ] 轉換，然後將綠色箭頭拖曳至新的 [ **一般檔案目的地**]。  
  
4.  在 **[資料流程]** 設計介面中，於新加入的 **[一般檔案目的地]** 轉換中按一下 **[一般檔案目的地]** ，並將名稱變更為 **「失敗的資料列」**。  
  
5.  以滑鼠右鍵按一下 **[失敗的資料列]** 轉換，然後按一下 **[編輯]**，再按一下 **[一般檔案目的地編輯器]** 中的 **[新增]**。  
  
6.  在 **[一般檔案格式]** 對話方塊中，確認已選取 **[使用分隔符號]** ，然後按一下 **[確定]**。  
  
7.  在 **一般檔案連接管理員編輯器**，請在**連接管理員名稱**方塊中，輸入`Error Data`。  
  
8.  在 **[一般檔案連接管理員編輯器]** 對話方塊中，按一下 **[瀏覽]**，並尋找儲存該檔案的資料夾。  
  
9. 中**開放**] 對話方塊中，如**檔案名稱**，型別`ErrorOutput.txt`，然後按一下 [**開啟**。  
  
10. 在 **[一般檔案連接管理員編輯器]** 對話方塊中，確認 **[地區設定]** 方塊包含 [英文 (美國)]， **[字碼頁]** 包含 1252 [ANSI - 拉丁文 1]。  
  
11. 在 [選項] 窗格中，按一下 **[資料行]**。  
  
     請注意，除了來源資料檔的資料行之外，還出現三個新的資料行：ErrorCode、ErrorColumn 和 ErrorDescription。 這些資料行是由 [查閱貨幣索引鍵] 轉換的錯誤輸出和 [取得錯誤描述] 轉換中的指令碼產生，而且可用來找出失敗資料列的原因並加以解決。  
  
12. 按一下 [確定] 。  
  
13. 在 **[一般檔案目的地編輯器]** 中，清除 **[覆寫檔案中的資料]** 核取方塊。  
  
     清除這個核取方塊可保存多次封裝執行的錯誤。  
  
14. 在 **[一般檔案目的地編輯器]** 中，按一下 **[對應]** 來確認所有資料行都正確。 您可以選擇性地重新命名目的地的資料行。  
  
15. 按一下 [確定] 。  
  
## <a name="next-steps"></a>後續步驟  
 [步驟 5：測試第 4 課的教學課程套件](../integration-services/lesson-4-5-testing-the-lesson-4-tutorial-package.md)  
  
  

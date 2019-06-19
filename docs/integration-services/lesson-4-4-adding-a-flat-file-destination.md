---
title: 步驟 4：新增一般檔案目的地 | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: f4088de3-16d8-419c-96a1-a2cd005d0a5b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0c13a761087cb263983a8d99b27514fcb225d93a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65721446"
---
# <a name="lesson-4-4-add-a-flat-file-destination"></a>課程 4-4：新增一般檔案目的地

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



[查閱貨幣索引鍵] 轉換的錯誤輸出會將任何導致查閱失敗的資料列，重新導向到 [指令碼] 轉換作業。 為了提供有關所發生錯誤的詳細資訊，[指令碼] 轉換會執行一個可取得每個錯誤之描述的指令碼。  
  
在此工作中，您會將與失敗資料列相關的所有資訊，儲存至分隔符號文字檔中以供稍後處理。 為了儲存失敗的資料列，您需為包含錯誤資料的文字檔，新增及設定「一般檔案」連線管理員和「一般檔案」目的地。 透過設定「一般檔案」目的地使用之「一般檔案」連接管理員上的屬性，您可以指定「一般檔案」目的地如何格式化並寫入文字檔。 如需詳細資訊，請參閱[一般檔案連線管理員](../integration-services/connection-manager/flat-file-connection-manager.md)和[一般檔案目的地](../integration-services/data-flow/flat-file-destination.md)。  
  
## <a name="add-and-configure-a-flat-file-destination"></a>新增及設定一般檔案目的地  
  
1.  選取 [資料流程]  索引標籤。  
  
2.  在 **[SSIS 工具箱]** 中，展開 [其他目的地]  ，然後將 [一般檔案目的地]  拖曳至資料流程設計介面上。 將 **[一般檔案目的地]** 直接放在 **[取得錯誤描述]** 轉換之下。  
  
3.  選取 [取得錯誤描述]  轉換，然後將藍色箭頭拖曳至新的 [一般檔案目的地]  。  
  
4.  在 [資料流程]  設計介面上，於新的 [一般檔案目的地]  轉換中選取 [一般檔案目的地]  名稱，然後將該名稱變更為**失敗的資料列**。  
  
5.  在 [失敗的資料列]  轉換上按一下滑鼠右鍵，選取 [編輯]  ，然後在 [一般檔案目的地編輯器]  中，選取 [新增]  。  
  
6.  在 [一般檔案格式]  對話方塊中，確認已選取 **[使用分隔符號]** ，然後選取 [確定]  。  
  
7.  在 [一般檔案連線管理員編輯器]  的 **[連線管理員名稱]** 方塊中，輸入 *Error Data*。  
  
8.  在 [一般檔案連線管理員編輯器]  對話方塊中，選取 [瀏覽]  ，然後尋找要儲存該檔案的資料夾。  
  
9. 在 [開啟]  對話方塊的 [檔案名稱]  中，輸入 *ErrorOutput.txt*，然後選取 [開啟]  。  
  
10. 在 [一般檔案連線管理員編輯器]  對話方塊中，確認 [地區設定]  方塊是 [英文 (美國)]  ，[字碼頁]  是 [1252 (ANSI - 拉丁文 I)]  。  
  
11. 在選項窗格中，選取 [資料行]  。  
  
    除了來自來源資料檔的資料行之外，還有三個新的資料行：ErrorCode、ErrorColumn 和 ErrorDescription。 這些資料行是 [查閱貨幣索引鍵] 轉換及 [取得錯誤描述] 轉換中之指令碼的錯誤輸出。 您可以使用這些資料行，針對失敗資料列的原因進行疑難排解。  
  
12. 選取 [確定]  。  
  
13. 在 **[一般檔案目的地編輯器]** 中，清除 **[覆寫檔案中的資料]** 核取方塊。  
  
    如果將此核取方塊取消選取，將可藉由附加每個新執行項的錯誤輸出，讓錯誤跨多次套件執行保存下來。
  
14. 在 [一般檔案目的地編輯器]  中，選取 [對應]  以確認所有資料行都正確。 您可以選擇性地重新命名目的地的資料行。  
  
15. 選取 [確定]  。  
  
## <a name="go-to-next-task"></a>移至下一個工作
[步驟 5：測試第 4 課教學課程套件](../integration-services/lesson-4-5-testing-the-lesson-4-tutorial-package.md)  
  
  
  

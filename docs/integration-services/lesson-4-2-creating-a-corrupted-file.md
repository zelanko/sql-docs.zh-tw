---
title: 步驟 2:建立損毀的檔案 | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: cd0b18dc-66c3-4d88-86ef-8e40cb660fae
author: janinezhang
ms.author: janinez
ms.openlocfilehash: d7601ba8a9cdb05372b27358488ab7f621a65809
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68055838"
---
# <a name="lesson-4-2-create-a-corrupted-file"></a>課程 4-2：建立損毀的檔案

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



為了示範設定和轉換錯誤的處理，您需要一個在處理時會造成元件失敗的範例一般檔案。  
  
在此工作中，您會建立現有範例一般檔案的複本。 接著，您會在「記事本」中開啟該檔案並編輯 **CurrencyID** 資料行，以包含讓查閱失敗的錯誤值。 當處理損毀的檔案時，查閱失敗會導致 [貨幣索引鍵查閱] 轉換失敗，因而使得套件的其餘部分也失敗。 在您建立損毀的範例檔案之後，需執行套件來檢視套件失敗。  
  
## <a name="create-a-corrupted-sample-flat-file"></a>建立損毀的範例一般檔案  
  
1.  在「記事本」或任何其他文字編輯器中，開啟 **Currency_VEB.txt** 檔案。  
  
2.  使用文字編輯器的尋找和取代功能，來尋找 **VEB** 的所有執行個體，並以 **BAD**取代。  
  
3.  在與其他範例資料檔案相同的資料夾中，將已修改的檔案另存為 **Currency_BAD.txt**。  
  
    > [!NOTE]  
    > 請務必將 **Currency_BAD.txt** 儲存在與其他範例資料檔案相同的資料夾中。  
  
4.  關閉文字編輯器。  
  
## <a name="verify-that-an-error-occurs-during-run-time"></a>確認在執行階段會發生錯誤  
  
1.  在 [偵錯]  功能表上，選取 [開始偵錯]  。  
  
    在資料流程的第三次反覆運算中，[查閱貨幣索引鍵] 轉換會嘗試處理 **Currency_BAD.txt** 檔案，但轉換會失敗。 轉換失敗會造成整個套件失敗。  
  
2.  在 [偵錯]  功能表上，選取 [停止偵錯]  。  
  
3.  在設計介面上，選取 [執行結果]  索引標籤。  
  
4.  瀏覽記錄並確認已發生下列無法處理的錯誤：  
  
    ```
    [Lookup Currency Key[27]] Error: Row yielded no match during lookup.
    ```
  
    > [!NOTE]  
    > 數字 27 是元件的識別碼。 當您建立資料流程時會指派此值，您封裝中的值可能不同。  
  
## <a name="go-to-next-task"></a>移至下一個工作  
[步驟 3：新增錯誤流程重新導向](../integration-services/lesson-4-3-adding-error-flow-redirection.md)  
  
  
  

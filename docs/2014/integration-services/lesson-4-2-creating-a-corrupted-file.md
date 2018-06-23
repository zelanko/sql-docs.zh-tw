---
title: 步驟 2：建立損毀的檔案 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: cd0b18dc-66c3-4d88-86ef-8e40cb660fae
caps.latest.revision: 23
author: douglaslM
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 80961e5899162575ae832d5d6a8dd35824b43a49
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36036371"
---
# <a name="step-2-creating-a-corrupted-file"></a>步驟 2：建立損毀檔案
  若要示範組態和轉換錯誤的處理，您必須建立處理時會造成元件失敗的範例一般檔案。  
  
 在這項工作中，您會建立現有的範例一般檔案的副本。 然後您會在記事本開啟檔案及編輯 [CurrencyID] 資料行，以確定在轉換查閱期間，它無法產生相符者。 在處理新檔案時，查閱失敗會造成 [貨幣索引鍵查閱] 轉換失敗，因而使得其餘的封裝也失敗。 在您建立損毀範例檔案之後，將執行封裝來檢視封裝失敗。  
  
### <a name="to-create-a-corrupted-sample-flat-file"></a>若要建立損毀範例一般檔案  
  
1.  在記事本或任何其他文字編輯器中開啟 Currency_VEB.txt 檔。  
  
     範例資料隨附在 SSIS 課程封裝中。 若要下載範例資料和課程封裝，請執行下列動作。  
  
    1.  巡覽至 [Integration Services 產品範例](http://go.microsoft.com/fwlink/?LinkID=267527)。  
  
    2.  按一下 **[下載]** 索引標籤。  
  
    3.  按一下 SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip 檔案。  
  
2.  使用文字編輯器的尋找和取代功能，來尋找所有執行個體`VEB`並將其取代為`BAD`。  
  
3.  在與其他範例資料檔相同資料夾中，將已修改的檔案儲存為`Currency_BAD.txt`。  
  
    > [!IMPORTANT]  
    >  請確定`Currency_BAD.txt`儲存為其他範例資料檔案相同的資料夾。  
  
4.  關閉文字編輯器。  
  
### <a name="to-verify-that-an-error-will-occur-during-run-time"></a>若要確認在執行階段會發生錯誤  
  
1.  在 **[偵錯]** 功能表上，按一下 **[開始偵錯]**。  
  
     在資料流程的第三次反覆運算中，[查閱貨幣索引鍵] 轉換會嘗試處理 Currency_BAD.txt 檔，但轉換會失敗。 轉換失敗將造成整個封裝失敗。  
  
2.  在 **[偵錯]** 功能表上，按一下 **[停止偵錯]**。  
  
3.  在設計介面中，按一下 [執行結果] 索引標籤。  
  
4.  瀏覽記錄並確認已發生下列無法處理的錯誤：  
  
     `[Lookup Currency Key[27]] Error: Row yielded no match during lookup.`  
  
    > [!NOTE]  
    >  數字 27 是元件的識別碼。 當您建立資料流程時會指派此值，您封裝中的值可能不同。  
  
## <a name="next-steps"></a>後續步驟  
 [步驟 3： 加入錯誤流程重新導向](lesson-4-3-adding-error-flow-redirection.md)  
  
  
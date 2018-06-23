---
title: 工作 4： 管理和檢視結果 |Microsoft 文件
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ecc3ba7e-fecf-478f-8825-6e4764b00e99
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 0e045d9722d380af19147746944c842f97ac9843
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36146206"
---
# <a name="task-4-manaing-and-viewing-results"></a>工作 4：管理和檢視結果
  在這項工作中，您會檢閱電腦輔助清理的結果，同時針對供應商資料執行互動式清理。 請參閱[互動式清理階段](http://msdn.microsoft.com/library/hh213061.aspx#Interactive)如需詳細資訊。  
  
1.  選取**Contact Email**網域的網域清單。  
  
2.  切換至**無效**右窗格中的索引標籤。 請注意在結尾遺漏 ‘s’ 字元的兩個電子郵件地址。 找不到無效的定義域規則需要以結尾的所有電子郵件地址這些兩個電子郵件**@adventure-works.com** (使用的 ')。 DQS 會在清理時使用此定義域規則，以判斷電子郵件是否有效。 此索引標籤會顯示在知識庫中標示為無效或未能通過定義域規則的定義域值。 在此情況下，這些值未通過定義域規則 (電子郵件驗證)。  
  
3.  在**更正為**資料行中輸入正確的電子郵件地址結尾為**@adventure-works.com** (使用的 ')。  
  
     ![從電子郵件驗證規則的更正](../../2014/tutorials/media/et-managingandviewingresults-01.jpg "更正電子郵件驗證規則")  
  
4.  按一下**核准**核准的變更記錄。 當您核准時，記錄就會移至**更正** 索引標籤。而不是個別核准每個項目，您可以核准一次使用的所有變更**都核准所有詞彙**工具列按鈕。  
  
5.  切換至**新增**右窗格中的索引標籤。 此索引標籤的值是 DQS 在知識庫中還沒有足夠資訊的值，因此無法判斷這些值是否正確。 因此，它無法變更或建議定義域值的變更。  
  
6.  檢閱這些值來確認所有電子郵件結尾**@adventure-works.com**按一下**核准所有詞彙**工具列上。 核准的值會從這個索引標籤移至**更正** 索引標籤。  
  
7.  選取**國家/地區**網域的網域清單。  
  
8.  切換至**更正**右窗格中的索引標籤，並注意**United State**值已自動更正為**美國**使用的 ' 結尾。 此規則不是您定義的規則**國家/地區**網域，但是 DQS 有**83%** 確定正確的值是**美國**。 **核准**按鈕會自動選取所有**更正**項目。 您可以覆寫這個行為並拒絕變更。  
  
9. 請注意， **USA**更正為**美國**因為它們是同義字和**美國**是前置 （慣用） 值。  
  
     ![更正根據同義字](../../2014/tutorials/media/et-managingandviewingresults-02.jpg "更正根據同義字")  
  
10. 請注意，**核准**按鈕都已選取這些更正值。 這是更正值的預設行為。 您可以拒絕變更，而且當您這樣做時，此值會移至**無效** 索引標籤。  
  
11. 選取**Supplier Name**從網域清單。  
  
12. 切換至**更正**右窗格中的索引標籤。  
  
     ![已更正的供應商名稱](../../2014/tutorials/media/et-managingandviewingresults-03.jpg "更正供應商名稱")  
  
    1.  請注意， **A.Datum Corp.** 更正為**A.Datum Corporation**和**原因**設**詞彙為主的關聯。A.datum Corporation**是 DQS 已知的定義域值，因為它在知識探索程序期間偵測到。 因此，DQS 是**100%的信心**對於這項更正。  
  
    2.  請注意， **Lazy Country Storex**更正為**Lazy Country Store**，**信心層級**設為**100%**，和**原因**設**定義域值**。 在知識探索程序期間設定**Lazy Country Storex**包含的錯誤形式**Lazy Country Store**為**更正**，所以 DQS 是**100%確信已經**有關進行這項更正。  
  
    3.  DQS 不熟悉清單中的其他值，但是找到使用這些值的更正**拼字檢查工具**以及建議適當的修正。 DQS 是**不是 100%** 對於這些更正，但信心層級高於 80%，也就是進行修正，所以 DQS 提議更正的臨界值層級。  
  
13. 請注意，**核准**會自動啟用的所有值。 您可依適當情況覆寫更正值或拒絕變更。 根據預設**核准**按鈕上選取了 [所有值**更正**] 索引標籤。  
  
14. 切換至**新增** 索引標籤。  
  
15. 請注意， **Corp.** 更正為**Corporation**， **Co.** 更正為**公司**，和**Inc.** 更正為**Incorporated**。 例如， **Consolidate Inc.** 更正為**Consolidate Incorporated**和**Consolidated Co.** 更正為**Consolidated Company**，和**Frabrikam Corp.** 更正為**Fabrikam Corporation**。  您可以看到**以詞彙為主的關聯性**提及是原因。 這些變更是使用您在定義域管理活動期間所定義之以詞彙為主的關聯所建議。 您可以變更**更正為**這裡手動值。  
  
16. 捲動清單，請參閱**Hunxgry Coyote Store**具有紅色曲線。 以滑鼠右鍵按一下它，然後按一下**Hungy Coyote Store** （以沒有 ' x')。 **更正為**資料行應該自動填入**Hungry Coyote Store**。 您也可以在 [更正為] 資料行中手動輸入值。  
  
17. 按一下**核准所有詞彙**從工具列。 定義域值**更正為**指定值移至**更正** 索引標籤並沒有相關聯的新值**更正為**值移至**正確** 索引標籤。  
  
18. 選取**地址驗證**網域清單從複合定義域。  
  
19. 在右窗格中，切換至**更正** 索引標籤。您應該會看到所找到不正確地址**Melissa Data – Address Check** DQS 服務上**Azure Marketplace**。  
  
20. 切換至**更正** 索引標籤。  
  
21. 請注意，**狀態**記錄具有**縣 （市)** 為**洛杉磯**設**CA**現在。 請注意，在**原因**欄位是 **' City-State Rule' 規則更正**。  
  
     ![City-State 規則更正](../../2014/tutorials/media/et-managingandviewingresults-04.jpg "City-State 規則更正")  
  
22. 請注意，**核准**選項按鈕已選取此項目的清單中。 這是預設行為的項目上**更正** 索引標籤。  
  
23. 切換至**建議** 索引標籤。檢閱所建議的變更**Melissa Data – Address Check**服務。  
  
24. **按一下 核准所有詞彙** 工具列按鈕，按一下都 **確定**上**確認**訊息方塊。  
  
     ![核准所有詞彙 工具列按鈕](../../2014/tutorials/media/et-managingandviewingresults-05.jpg "都核准所有詞彙 工具列按鈕")  
  
25. 按一下**下一步**切換至**匯出**頁面。  
  
## <a name="next-step"></a>下一個步驟  
 [工作 5： 匯出清理結果到 Excel 檔案](../../2014/tutorials/task-5-exporting-cleansing-results-to-an-excel-file.md)  
  
  
---
title: 工作 4：管理和檢視結果 |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: ecc3ba7e-fecf-478f-8825-6e4764b00e99
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 2df7517a8043269efe40d21b112100edaf9e847f
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/09/2019
ms.locfileid: "65489450"
---
# <a name="task-4-manaing-and-viewing-results"></a>工作 4：管理和檢視結果
  在這項工作中，您會檢閱電腦輔助清理的結果，同時針對供應商資料執行互動式清理。 請參閱[互動式清理階段](https://msdn.microsoft.com/library/hh213061.aspx#Interactive)如需詳細資訊。  
  
1.  選取 [ **Contact Email**網域的網域清單。  
  
2.  若要切換**無效**右窗格中的索引標籤。 請注意，兩個電子郵件地址的遺漏字元 ' 結尾。 找不到為無效的定義域規則需要所有的電子郵件地址結尾為這些兩個電子郵件 **@adventure-works.com** (使用的 ')。 DQS 會在清理時使用此定義域規則，以判斷電子郵件是否有效。 此索引標籤會顯示在知識庫中標示為無效或未能通過定義域規則的定義域值。 在此情況下，這些值未通過定義域規則 (電子郵件驗證)。  
  
3.  在 [**更正為**資料行中輸入正確的電子郵件地址結尾 **@adventure-works.com** (使用的 ')。  
  
     ![從電子郵件驗證規則的更正](../../2014/tutorials/media/et-managingandviewingresults-01.jpg "更正電子郵件驗證規則")  
  
4.  按一下 [**核准**核准的變更記錄。 當您核准時，記錄會移至**更正**] 索引標籤。而不是個別核准每個項目，您可以核准使用一次的所有變更**都核准所有詞彙**工具列按鈕。  
  
5.  若要切換**新增**右窗格中的索引標籤。 此索引標籤的值是 DQS 在知識庫中還沒有足夠資訊的值，因此無法判斷這些值是否正確。 因此，它無法變更或建議定義域值的變更。  
  
6.  檢閱這些值來確認所有電子郵件結尾 **@adventure-works.com** 然後按一下 **核准所有詞彙** 工具列上。 核准的值會從這個索引標籤移至 **更正**] 索引標籤。  
  
7.  選取 [**國家/地區** 網域的網域清單。  
  
8.  切換至**更正**索引標籤上，在右窗格中，並注意**United State**值已自動更正為**美國**使用的 ' 結尾。 此規則不是您定義的規則**國家/地區**網域，但是 DQS 有**83%** 確定正確的值是**美國**。 **核准**] 按鈕會自動選取所有**更正**項目。 您可以覆寫這個行為並拒絕變更。  
  
9. 請注意， **USA**更正為**美國**因為它們是同義字並**美國**是前置 （慣用） 值。  
  
     ![修正根據同義字](../../2014/tutorials/media/et-managingandviewingresults-02.jpg "修正根據同義字")  
  
10. 請注意，**核准**按鈕都已選取這些更正值。 這是更正值的預設行為。 您可以拒絕變更，而且當您這樣做時，此值會移至**無效**] 索引標籤。  
  
11. 選取 [ **Supplier Name**從網域清單。  
  
12. 若要切換**更正**右窗格中的索引標籤。  
  
     ![已更正的供應商名稱](../../2014/tutorials/media/et-managingandviewingresults-03.jpg "更正供應商名稱")  
  
    1.  請注意， **A.Datum Corp.** 更正為**A.Datum Corporation**並**原因**設為**詞彙為主的關聯。A.datum Corporation**是 DQS 已知的定義域值，因為它已在知識探索程序期間探索到。 因此，DQS 就**100%的信心**這項更正。  
  
    2.  請注意， **Lazy Country Storex**更正為**Lazy Country Store**，**信心層級**設定為**100%**，以及**原因**設定為**定義域值**。 在您設定在知識探索程序期間**Lazy Country Storex**為錯誤而**Lazy Country Store**作為**更正**，因此，DQS **100%有信心**有關進行這項更正。  
  
    3.  DQS 不熟悉的其他值，在清單中，但它找到使用這些值的更正**拼字檢查工具**以及建議適當的修正。 DQS 是**不是 100%** 十分熟悉這些修正，但信心層級高於 80%，也就是進行修正，因此 DQS 提議更正的臨界值層級。  
  
13. 請注意，**核准**會自動啟用的所有值。 您可依適當情況覆寫更正值或拒絕變更。 依預設**核准**] 按鈕上選取的所有值**更正**] 索引標籤。  
  
14. 若要切換**新增**] 索引標籤。  
  
15. 請注意， **Corp.** 更正為**Corporation**， **Co.** 更正為**公司**，和**Inc.** 來更正**Incorporated**。 例如， **Consolidate Inc.** 更正為**Consolidate Incorporated**並**Consolidated Co.** 更正為**Consolidated Company**，並**Frabrikam Corp.** 更正為**Fabrikam Corporation**。  您可以看到**以詞彙為主的關聯性**提及是原因所在。 這些變更是使用您在定義域管理活動期間所定義之以詞彙為主的關聯所建議。 您可以變更**更正為**手動這裡值。  
  
16. 捲動清單，請參閱**Hunxgry Coyote Store**具有紅色波浪線。 以滑鼠右鍵按一下它，然後按一下 [ **Hungy Coyote Store** （以沒有 ' x')。 **更正為**資料行應該會自動填入**Hungry Coyote Store**。 您也可以在 [更正為] 資料行中手動輸入值。  
  
17. 按一下 [**核准所有詞彙**從工具列。 定義域值**更正為**指定的值移至**更正**索引標籤，並沒有相關聯的新值**更正為**值移至**正確**] 索引標籤。  
  
18. 選取 [**地址驗證**從網域清單的複合定義域。  
  
19. 在右窗格中，切換至**更正**] 索引標籤。您應該會看到正確地找到的地址**Melissa Data – Address Check** DQS 服務**Azure Marketplace**。  
  
20. 若要切換**更正**] 索引標籤。  
  
21. 請注意，**狀態**所具有的記錄**城市**做為**Los Angeles**設定為**CA**現在。 請注意，在**原因**欄位是**被 ' City-State Rule' 規則更正**。  
  
     ![City-State 規則更正](../../2014/tutorials/media/et-managingandviewingresults-04.jpg "City-State 規則更正")  
  
22. 請注意，**核准**已為此項目清單中選取選項按鈕。 這是預設行為的項目上**更正**] 索引標籤。  
  
23. 若要切換**建議**] 索引標籤。檢閱所建議的變更**Melissa Data – Address Check**服務。  
  
24. **按一下 [核准所有詞彙**工具列按鈕，然後按一下都 [ **[確定]** 上**確認**訊息方塊。  
  
     ![核准所有詞彙] 工具列按鈕](../../2014/tutorials/media/et-managingandviewingresults-05.jpg "都核准所有詞彙] 工具列按鈕")  
  
25. 按一下 [**下一步**轉為**匯出**頁面。  
  
## <a name="next-step"></a>下一個步驟  
 [工作 5:匯出清理結果到 Excel 檔案](../../2014/tutorials/task-5-exporting-cleansing-results-to-an-excel-file.md)  
  
  

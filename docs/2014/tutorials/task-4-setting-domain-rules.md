---
title: 工作4：設定定義域規則 |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 3a7162ba-cf2f-481f-830d-bb6a02823827
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: dd59bf315e90bd52ba1388d27c533ab4a3136d3c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "72381735"
---
# <a name="task-4-setting-domain-rules"></a>工作 4：設定定義域規則
  在這項工作中，您會建立**連絡人電子郵件**網域的規則，以驗證電子郵件地址的結尾是否為** \@adventure-works.com**。 如需此頁面的詳細資訊，請參閱[建立定義域規則](https://msdn.microsoft.com/library/hh510397.aspx)主題。  
  
1.  按一下 [**網域] 清單**中的 [**連絡人電子郵件**]。  
  
2.  切換至右窗格中的 [**定義域規則**] 索引標籤。  
  
     ![[加入新的定義域規則] 工具列按鈕](../../2014/tutorials/media/et-settingdomainrules-01.jpg "[加入新的定義域規則] 工具列按鈕")  
  
3.  在右窗格中，按一下工具列上的 [**加入新的定義域規則**] 按鈕（請參閱影像）以新增規則。  
  
4.  輸入 [**規則名稱**的**電子郵件驗證**]，然後按**enter**。 [作用中] 核取方塊預設為核取**狀態**。 這個控制項可讓您暫時停用規則。  
  
5.  在 [**建立規則**] 窗格中，按一下**向下箭**號，然後選取 [**值結尾為**]。  
  
6.  在文字方塊中輸入** \@adventure-works.com** ，然後按**tab**鍵。 您可以在 [**建立規則**] 窗格中，按一下 **[將新條件新增至選取的子句**] 工具列按鈕來新增更多條件。  
  
     ![電子郵件驗證規則](../../2014/tutorials/media/et-settingdomainrules-02.jpg "電子郵件驗證規則")  
  
7.  在右窗格中，按一下工具列上的 **[在測試資料上執行選取的定義域規則**] 按鈕，對範例資料測試規則。  
  
     ![[在測試資料上執行定義域規則] 工具列按鈕](../../2014/tutorials/media/et-settingdomainrules-03.jpg "[在測試資料上執行定義域規則] 工具列按鈕")  
  
8.  在 [**測試定義域規則**] 對話方塊中，按一下工具列上**的 [加入定義域規則的新測試詞彙**] 按鈕。  
  
     ![[測試定義域規則] 對話方塊](../../2014/tutorials/media/et-settingdomainrules-04.jpg "[測試定義域規則] 對話方塊")  
  
9. 在 [**連絡人電子郵件**] 資料行中輸入**\@frank7 adventure-works.com** （有效的值）。  
  
10. 重複先前的兩個步驟，以新增**joe2\@adventure-work.com** （不含 ' s ' 的無效值）。  
  
11. 按一下工具列上的 [最後一個] 按鈕（**針對所有詞彙測試定義域規則**），以根據規則測試輸入資料。  
  
     ![[對所有詞彙測試定義域規則] 工具列按鈕](../../2014/tutorials/media/et-settingdomainrules-05.jpg "[對所有詞彙測試定義域規則] 工具列按鈕")  
  
12. 請注意，第一個輸入顯示為有效的項目，第二個輸入則顯示為無效的項目。  
  
     ![測試定義域規則結果](../../2014/tutorials/media/et-settingdomainrules-06.jpg "測試定義域規則結果")  
  
13. 按一下 [**關閉**] 以關閉 [**測試定義域規則**] 對話方塊。  
  
## <a name="next-step"></a>後續步驟  
 [工作 5：設定以詞彙為主的關聯](../../2014/tutorials/task-5-setting-term-based-relationships.md)  
  
  

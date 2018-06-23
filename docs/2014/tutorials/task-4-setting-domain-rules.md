---
title: 工作 4： 設定定義域規則 |Microsoft 文件
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
ms.assetid: 3a7162ba-cf2f-481f-830d-bb6a02823827
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 89e0027b3bf1748fb68a8b6922c45572a7b41bb7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36033799"
---
# <a name="task-4-setting-domain-rules"></a>工作 4：設定定義域規則
  在這項工作，您建立的規則**Contact Email**網域來驗證是否電子郵件地址結尾為**@adventure-works.com**。 請參閱[建立定義域規則](http://msdn.microsoft.com/library/hh510397.aspx)更多詳細資料頁面上的主題。  
  
1.  按一下**Contact Email**中**網域清單**。  
  
2.  切換至**定義域規則**右窗格中的索引標籤。  
  
     ![加入新的定義域規則 工具列按鈕](../../2014/tutorials/media/et-settingdomainrules-01.jpg "加入新的定義域規則 工具列按鈕")  
  
3.  在右窗格中，按一下 **加入新的定義域規則**工具列上的按鈕 （請參閱影像） 加入規則。  
  
4.  型別**電子郵件驗證**如**規則名稱**按**ENTER**。 **Active**預設應該會核取核取方塊。 這個控制項可讓您暫時停用規則。  
  
5.  在**建置規則**] 窗格中，按一下 [**向下箭號**，然後選取**值結尾為**。  
  
6.  型別**@adventure-works.com**中文字 方塊，然後按** 索引標籤**。 您可以加入更多條件，即可**新條件加入選取的子句**中的工具列按鈕**建置規則**窗格。  
  
     ![電子郵件驗證規則](../../2014/tutorials/media/et-settingdomainrules-02.jpg "電子郵件驗證規則")  
  
7.  按一下**測試資料上執行選取的定義域規則**中測試規則針對取樣資料的右窗格的工具列上的按鈕。  
  
     ![在測試資料 工具列按鈕上執行定義域規則](../../2014/tutorials/media/et-settingdomainrules-03.jpg "上測試資料 工具列按鈕執行定義域規則")  
  
8.  在**測試定義域規則**對話方塊中，按一下 **加入定義域規則的新測試詞彙**工具列上的按鈕。  
  
     ![測試定義域規則 對話方塊](../../2014/tutorials/media/et-settingdomainrules-04.jpg "測試定義域規則 對話方塊")  
  
9. 型別**frank7@adventure-works.com** （有效值） 中**Contact Email**資料行。  
  
10. 重複上述兩個步驟來加入**joe2@adventure-work.com** (不含無效的值的 ')。  
  
11. 按一下最後一個按鈕 (**對所有詞彙測試定義域規則**) 測試輸入的資料依規則 工具列上。  
  
     ![測試定義域規則的所有詞彙 工具列按鈕](../../2014/tutorials/media/et-settingdomainrules-05.jpg "測試定義域規則的所有詞彙 工具列按鈕")  
  
12. 請注意，第一個輸入顯示為有效的項目，第二個輸入則顯示為無效的項目。  
  
     ![測試定義域規則結果](../../2014/tutorials/media/et-settingdomainrules-06.jpg "測試定義域規則結果")  
  
13. 按一下**關閉**關閉**測試定義域規則** 對話方塊。  
  
## <a name="next-step"></a>下一個步驟  
 [工作 5： 設定以詞彙為主的關聯性](../../2014/tutorials/task-5-setting-term-based-relationships.md)  
  
  
---
title: 工作 4:設定定義域規則 |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 3a7162ba-cf2f-481f-830d-bb6a02823827
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: f8816afcf44bdcb38f6513f61b3b88ce505dedc7
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56035309"
---
# <a name="task-4-setting-domain-rules"></a>工作 4:設定定義域規則
  在這個工作中，您建立的規則**Contact Email**網域來驗證是否電子郵件地址結尾**@adventure-works.com**。 請參閱[建立定義域規則](https://msdn.microsoft.com/library/hh510397.aspx)如需詳細資料頁面上的主題。  
  
1.  按一下  **Contact Email**中**定義域清單**。  
  
2.  若要切換**定義域規則**右窗格中的索引標籤。  
  
     ![加入新的定義域規則 工具列按鈕](../../2014/tutorials/media/et-settingdomainrules-01.jpg "新增新的定義域規則 工具列按鈕")  
  
3.  在右窗格中，按一下**加入新的定義域規則**工具列上的按鈕 （請參閱映像） 新增規則。  
  
4.  型別**電子郵件驗證**for**規則名稱**然後按**ENTER**。 **Active**預設應該核取核取方塊。 這個控制項可讓您暫時停用規則。  
  
5.  在**建立規則**窗格中，按一下**向下箭號**，然後選取**值結尾為**。  
  
6.  型別**@adventure-works.com**文字方塊中，然後按下**索引標籤**。 您可以加入更多條件，依序按一下**將新條件加入選取的子句**中的工具列按鈕**建置規則**窗格。  
  
     ![電子郵件驗證規則](../../2014/tutorials/media/et-settingdomainrules-02.jpg "電子郵件驗證規則")  
  
7.  按一下 **測試資料上執行選取的定義域規則**測試規則針對取樣資料的右窗格的工具列上的按鈕。  
  
     ![在 [測試資料] 工具列按鈕上執行定義域規則](../../2014/tutorials/media/et-settingdomainrules-03.jpg "測試資料 工具列按鈕上執行定義域規則")  
  
8.  在 [**測試定義域規則**] 對話方塊中，按一下**加入定義域規則的新測試詞彙**工具列上的按鈕。  
  
     ![測試定義域規則 對話方塊](../../2014/tutorials/media/et-settingdomainrules-04.jpg "測試定義域規則 對話方塊")  
  
9. 型別**frank7@adventure-works.com** （有效的值） 中**Contact Email**資料行。  
  
10. 重複上述兩個步驟來加入**joe2@adventure-work.com** (含無效值的 ')。  
  
11. 按一下最後一個按鈕 (**對所有詞彙測試定義域規則**) 測試輸入的資料依規則 工具列上。  
  
     ![測試定義域規則的所有詞彙 工具列按鈕](../../2014/tutorials/media/et-settingdomainrules-05.jpg "測試定義域規則的所有詞彙 工具列按鈕")  
  
12. 請注意，第一個輸入顯示為有效的項目，第二個輸入則顯示為無效的項目。  
  
     ![測試定義域規則結果](../../2014/tutorials/media/et-settingdomainrules-06.jpg "測試定義域規則結果")  
  
13. 按一下 **關閉 **以關閉**測試定義域規則** 對話方塊。  
  
## <a name="next-step"></a>下一個步驟  
 [工作 5:設定以詞彙為主的關聯性](../../2014/tutorials/task-5-setting-term-based-relationships.md)  
  
  

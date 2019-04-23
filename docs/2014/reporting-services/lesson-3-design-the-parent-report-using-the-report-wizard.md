---
title: 第 3 課：設計父報表使用報表精靈 |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 2f69dcd3-cd6d-45a9-a62a-ba6f5f3179d8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8fe60270cd3737e3c372fbf92ccb906beb8d06cb
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "59940233"
---
# <a name="lesson-3-design-the-parent-report-using-the-report-wizard"></a>第 3 課：使用報表精靈設計父報表
  在您建立父報表的資料連接和資料表之後，下一步是要使用報表設計師中的 [報表精靈] 設計父報表。 如需報表設計師的詳細資訊，請參閱[使用報表設計師設計報表 &#40;SSRS&#41;](tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md)。  
  
### <a name="to-design-the-parent-report-using-the-report-wizard"></a>若要使用報表精靈設計父報表  
  
1.  請確認已在 **方案總管**中選取頂層網站。  
  
2.  以滑鼠右鍵按一下網站，然後選取 [新增項目]。  
  
3.  在 **加入新項目**對話方塊中，選取**報表精靈**，輸入報表檔的名稱，然後按一下**新增**。  
  
     這樣會啟動 [報表精靈]。  
  
4.  在 **資料集屬性**頁面上，於**資料來源**方塊中，選取**DataSet1**您在建立[第 2 課：定義父報表的資料連接和資料表](lesson-2-define-a-data-connection-and-data-table-for-parent-report.md)。  
    [可用資料集] 方塊會自動更新為您如上所建立的 **DataTable**。  
  
5.  按一下 [下一步] 。  
  
6.  在 [排列欄位] 頁面中執行下列操作：  
  
    1.  從 [可用欄位] 將 **ProductID**、**Name**、**ProductNumber**、**SafetyStockLevel** 和 **ReorderLevel** 拖曳至 [值] 方塊。  
  
    2.  按一下箭號旁**sum （productid)**， **sum （safetystocklevel)**， **sum （reorderlevel)** 清除**總和**選取項目。  
  
7.  按一下 [**下一步]** 兩次，然後按一下**完成**以關閉**報表精靈**。  
  
     現在您已建立 .rdlc 檔。 此檔案會在報表設計師中開啟。 您設計的 Tablix 現在會顯示於設計介面中。  
  
8.  儲存 .rdlc 檔。  
  
## <a name="next-task"></a>下一項工作  
 您已使用 [報表精靈] 成功設計父報表。 接下來您將建立子報表的資料連接和資料表。  
  
  

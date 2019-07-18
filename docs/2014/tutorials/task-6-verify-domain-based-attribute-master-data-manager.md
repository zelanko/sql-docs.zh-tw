---
title: 工作 6：確認已建立使用主資料管理員的網域型屬性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 6e90517a-910c-4c33-8f11-92ac3cff4fdc
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: fe3f404d4f41e2977ef389216dcbc9106327266a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65488955"
---
# <a name="task-6-verify-that-the-domain-based-attribute-is-created-using-master-data-manager"></a>工作 6：確認已使用主資料管理員建立定義域屬性
  在這項工作中，您會透過 [主資料管理員]  來確認 **MDS** 中已建立 **State** 實體，而且 **Supplier** 實體的 **State** 屬性為相依於 **State** 實體的網域屬性。  
  
1.  切換到 [主資料管理員]  Web 應用程式。  
  
2.  按一下頂端的 [SQL Server 2012 Master Data Services]  ，回到首頁。  
  
3.  確定已選取 [Supplier]  模型，然後按一下 [總管]  。 如果您已經開啟 [總管]  ，可以重新整理頁面。  
  
4.  將滑鼠移**實體**功能表列並注意現在有兩個實體：**供應商**並**狀態**。  
  
     ![實體功能表使用的狀態和供應商](../../2014/tutorials/media/et-verifythatthedbaiscreatedusingmdm-01.jpg "狀態與供應商實體功能表")  
  
5.  按一下 [State]  (如果尚未開啟此實體)。  
  
6.  從清單中選取 [GA]  。  
  
7.  在右邊的 [詳細資料]  窗格中，將 [名稱]  變更為右窗格  的 **Georgia**，然後按一下 [確定]  。  
  
8.  針對其他州重複上述步驟。  
  
    |程式碼|名稱|  
    |----------|----------|  
    |CA|California|  
    |CO|Colorado|  
    |IL|Illinois|  
    |DC|District of Columbia|  
    |FL|Florida|  
    |AL|Alabama|  
    |KY|Kentucky|  
    |MA|Massachusetts|  
    |AZ|Arizona|  
    |MI|Michigan|  
    |MN|Minnesota|  
    |NJ|New Jersey|  
    |NV|Nevada|  
    |NY|New York|  
    |OH|Ohio|  
    |確定|Oklahoma|  
    |或|Oregon|  
    |PA|Pennsylvania|  
    |SC|South Carolina|  
    |KS|Kansas|  
    |TN|Tennessee|  
    |TX|Texas|  
    |UT|Utah|  
    |VA|Virginia|  
    |WA|Washington|  
    |WI|Wisconsin|  
    |HI|Hawaii|  
    |MD|Maryland|  
    |CT|Connecticut|  
  
9. 選取任何州，並從工具列按一下 [檢視交易]  。 您應該會看到您剛才更新的交易出現在交易清單中。  
  
10. 將滑鼠停留在 [實體]  功能表上方，並按一下 [Supplier]  。  
  
11. 現在，請注意可以使用下拉式清單在 [詳細資料]  窗格中變更 [State]  欄位的值。 您也可以看到，在左邊的清單中以及 [詳細資料]  窗格的下拉式清單中，都會先顯示代碼，然後是大括號中的名稱。 您也可以在 [詳細資料]  窗格中變更其他任何值。  
  
     ![狀態與更新的程式碼和名稱的屬性](../../2014/tutorials/media/et-verifythatthedbaiscreatedusingmdm-02.jpg "狀態與更新的程式碼和名稱的屬性")  
  
## <a name="next-step"></a>下一個步驟  
 [工作 7:檢視使用主資料管理員在 Excel 中進行更新](../../2014/tutorials/task-7-viewing-updates-made-using-master-data-manager-in-excel.md)  
  
  

---
title: 工作6：確認已使用主資料管理員建立網域屬性（Attribute） |Microsoft Docs
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
ms.openlocfilehash: 56418adbefec0dc996fd83ce70415e86ec9509a3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "78171658"
---
# <a name="task-6-verify-that-the-domain-based-attribute-is-created-using-master-data-manager"></a>工作 6：確認已使用主資料管理員建立定義域屬性
  在這項工作中，您會透過 [主資料管理員]**** 來確認 **MDS** 中已建立 **State** 實體，而且 **Supplier** 實體的 **State** 屬性為相依於 **State** 實體的網域屬性。

1.  切換到 [主資料管理員]**** Web 應用程式。

2.  按一下頂端的 [SQL Server 2012 Master Data Services]****，回到首頁。

3.  確定已選取 [Supplier]**** 模型，然後按一下 [總管]****。 如果您已經開啟 [總管]****，可以重新整理頁面。

4.  將滑鼠停留在功能表列的 [實體]**** 上方，並注意現在有兩個實體：**Supplier** 和 **State**。

     ![含 [省/市] 和 [供應商] 的 [實體] 功能表](../../2014/tutorials/media/et-verifythatthedbaiscreatedusingmdm-01.jpg "含 [省/市] 和 [供應商] 的 [實體] 功能表")

5.  按一下 [State]**** (如果尚未開啟此實體)。

6.  從清單中選取 [GA]****。

7.  在右邊的 [詳細資料]**** 窗格中，將 [名稱]**** 變更為右窗格**** 的 **Georgia**，然後按一下 [確定]****。

8.  針對其他州重複上述步驟。

    |程式碼|名稱|
    |----------|----------|
    |CA|California|
    |CO|Colorado|
    |IL|伊利諾州|
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
    |NY|紐約|
    |OH|Ohio|
    |[確定]|Oklahoma|
    |或者|Oregon|
    |PA|Pennsylvania|
    |SC|South Carolina|
    |KS|Kansas|
    |TN|Tennessee|
    |TX|Texas|
    |UT|Utah|
    |VA|維吉尼亞州|
    |WA|Washington|
    |WI|Wisconsin|
    |HI|Hawaii|
    |MD|Maryland|
    |CT|Connecticut|

9. 選取任何州，並從工具列按一下 [檢視交易]****。 您應該會看到您剛才更新的交易出現在交易清單中。

10. 將滑鼠停留在 [實體]**** 功能表上方，並按一下 [Supplier]****。

11. 現在，請注意可以使用下拉式清單在 [詳細資料]**** 窗格中變更 [State]**** 欄位的值。 您也可以看到，在左邊的清單中以及 [詳細資料]**** 窗格的下拉式清單中，都會先顯示代碼，然後是大括號中的名稱。 您也可以在 [詳細資料]**** 窗格中變更其他任何值。

     ![含 [更新代碼] 和 [名稱] 的屬性狀態](../../2014/tutorials/media/et-verifythatthedbaiscreatedusingmdm-02.jpg "含 [更新代碼] 和 [名稱] 的屬性狀態")

## <a name="next-step"></a>後續步驟
 [工作 7：檢視您在 Excel 中使用主資料管理員所做的更新](../../2014/tutorials/task-7-viewing-updates-made-using-master-data-manager-in-excel.md)



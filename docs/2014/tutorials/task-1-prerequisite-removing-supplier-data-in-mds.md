---
title: 工作 1 （必要條件）： 在 MDS 中移除供應商資料 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6f0a4287-7fd4-4f18-b7e4-a5191a9d4a3c
caps.latest.revision: 6
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d7cf9ccd921ecdef56560e712415604355b97b2f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37171999"
---
# <a name="task-1-prerequisite-removing-supplier-data-in-mds"></a>工作 1 (必要條件)：在 MDS 中移除供應商資料
  在這項工作中，您會移除儲存在 MDS 中的供應商資料。 使用以手動方式將資料上傳**MDS Excel 增益集**上一課。 您在這一課建立的 SSIS 封裝會將資料自動上傳至 MDS。 因此，在測試 SSIS 封裝之前，您必須從 MDS 中移除供應商資料、移除衍生階層、移除 supplier 和 state 實體，並且建立不含任何資料的 supplier 實體。  
  
1.  啟動**主資料管理員**瀏覽至**http://localhost/MDS**或網站和應用程式時指定設定 MDS。 如果您保留**主資料管理員**開啟，再按**SQL Server 2012 Master Data Services**若要切換至頂端**首頁**。  
  
2.  按一下 [**系統管理]** 中**系統管理工作**一節。  
  
3.  將滑鼠移**管理**功能表，然後按一下 **衍生階層**。 您需要刪除衍生的階層**SuppliersInState**之前刪除的實體**供應商**模型。  
  
4.  選取  **SuppliersInState**從**衍生階層**清單，然後按一下**X （刪除）** 工具列上的按鈕。  
  
5.  按一下 **確定**以確認刪除。  
  
6.  將滑鼠移**管理**功能表，然後按一下 **實體**。  
  
7.  按一下 **供應商**然後按一下**刪除 (X)** 工具列按鈕以刪除實體。 按一下 **確定**在訊息方塊上。  
  
8.  重複上述步驟來刪除**狀態**實體。  
  
9. 請不要關閉**主資料管理員**。  
  
10. 切換到 Excel 視窗具有**Cleansed and Matched Suppliers.xls**檔案開啟。 若要切換**Sheet1**底部的索引標籤。  
  
11. 選取 僅**第一個資料列包含標頭**。 請勿選取其他任何資料列。 您會想要根據 Excel 資料行建立實體，而不要上傳任何資料。 因此，您只選取有標頭的第一個資料列。  
  
12. 按一下 **主要資料**功能表列上。  
  
13. 按一下 **建立實體**從功能區。  
  
14. 在**管理連線** 對話方塊中，如果您看不到連接**本機 MDS 伺服器**之下**現有連接**，執行下列動作：  
  
    1.  選取 [**建立新的連接**，然後按一下**新增**] 按鈕。  
  
    2.  在 加入新連接 對話方塊中，輸入**本機 MDS 伺服器**如**描述**並**http://localhost/MDS**如**MDS 伺服器位址**，按一下 **確定**以關閉對話方塊。  
  
15. 在 **管理連接**對話方塊中，選取**本機 MDS 伺服器**(http://localhost/MDS)，按一下 **測試**來測試連線。 按一下 **確定**訊息方塊上。  
  
16. 按一下  **Connect**連接到 MDS 伺服器。  
  
17. 在 **建立實體**對話方塊方塊中，執行下列動作：  
  
    1.  確認**範圍**設為 **$1: $1**。  
  
    2.  選取 **供應商**for**模型**。  
  
    3.  選取  **VERSION_1** for**版本**。  
  
    4.  型別**供應商**for**新實體名稱**。  
  
    5.  選取  **SupplierID** for**程式碼**。  
  
    6.  選取  **Supplier Name** for**名稱**。  
  
    7.  按一下 **確定**來建立實體，然後關閉對話方塊。  
  
18. 關閉**Excel**並**不要儲存**檔案。  
  
19. 在 **主資料管理員**，重新整理網際網路瀏覽器，並確認**供應商**實體顯示在清單中。  
  
20. 若要切換**首頁**依序按一下**SQL Server 2012 Master Data Services**頂端。  
  
21. 確認**供應商**模型選取**模型**並**VERSION_1**選取**版本**。  
  
22. 按一下 **[總管]**。 請注意，**供應商**實體的所有屬性會透過**沒有任何值**。  
  
## <a name="next-step"></a>下一個步驟  
 [工作 2&#40;選擇性&#41;： 建立 MDS 訂閱檢視，使用主資料管理員](../../2014/tutorials/task-2-optional-creating-a-mds-subscription-view-using-master-data-manager.md)  
  
  

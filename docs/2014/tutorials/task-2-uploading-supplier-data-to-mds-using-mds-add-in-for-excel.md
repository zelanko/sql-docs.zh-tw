---
title: 工作 2： 將供應商資料上傳至 MDS 增益集使用適用於 Excel 的 MDS |Microsoft Docs
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
ms.assetid: 598deb57-e0cc-4e0a-aeb1-94432c094c67
caps.latest.revision: 6
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a296db8f933ceef5d3e17e2f3f3b8034cf8a0e2c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37272174"
---
# <a name="task-2-uploading-supplier-data-to-mds-using-mds-add-in-for-excel"></a>工作 2：使用適用於 Excel 的 MDS 增益集將供應商資料上傳到 MDS
  在這個工作中，您已清理和供應商將資料發佈至**MDS**使用**MDS 增益集適用於 Excel**。 建立名為實體**供應商**中**供應商**您在上一課中建立的模型。 此實體將會針對 Excel 檔案中的每個資料行具有一個屬性。 Supplier 實體的 Code 和 Name 屬性等於**SupplierID**並**Supplier Name**在 Excel 中的資料行。  
  
1.  開啟**清理和比對 Suppliers.xls**中**Excel**。  
  
2.  按下**CTRL + A**選取整個資料。 很**重要**試算表中，選取整個資料。  
  
3.  按一下 **主要資料**功能表列上。  
  
4.  按一下 **建立實體**功能區上的按鈕。  
  
     ![Excel-主要資料 索引標籤-[建立實體] 按鈕](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-01.jpg "Excel-主要資料索引標籤-[建立實體] 按鈕")  
  
5.  在**管理連線** 對話方塊中，如果您看不到連接**本機 MDS 伺服器**之下**現有連接**，執行下列動作：  
  
    1.  選取 [**建立新的連接**，然後按一下**新增**] 按鈕。  
  
    2.  中**加入新的連接** 對話方塊中，輸入**本機 MDS 伺服器**for**描述**並**http://localhost/MDS**的**MDS 伺服器位址**，然後按一下**確定**以關閉對話方塊。  
  
6.  在 **管理連接**對話方塊中，選取**本機 MDS 伺服器**(http://localhost/MDS)，按一下 **測試**來測試連線。 按一下 **確定**訊息方塊上。  
  
7.  按一下  **Connect**連接到 MDS 伺服器。  
  
8.  在 **建立實體**對話方塊中，選取**供應商**for**模型**。  
  
9. 請確認**VERSION_1**選取**版本**。  
  
10. 請輸入**供應商**for**新實體名稱**。  
  
11. 選取  **SupplierID** for**包含的唯一識別碼的資料行**欄位 （您也可以程式碼自動產生）。 您基本上對應**SupplierID**中的資料行**Excel**來**程式碼**屬性**供應商**實體。  
  
12. 選取  **Supplier Name** for**包含名稱的資料行**欄位。 您基本上對應**Supplier Name**中的資料行**Excel**來**名稱**屬性**供應商**實體。 **程式碼**並**名稱**屬性是在 MDS 中實體的必要屬性。  
  
     ![建立實體 對話方塊](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-02.jpg "建立實體 對話方塊")  
  
13. 按一下 [ **[確定]** 若要建立 MDS 的實體，將主要資料發佈到實體，並關閉**建立實體**] 對話方塊。  
  
14. 現在，您應該會看到標題為的新工作表**供應商**，這是實體，新增至 Excel 試算表的名稱，並且在工作表頂端您應該會看到工作表連接到 MDS 伺服器。 請注意，原始的工作表 (標題為**Sheet1**) 仍然存在。  
  
     ![Excel-供應商 和 Sheet1 索引標籤](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-03.jpg "Excel-供應商 和 Sheet1 索引標籤")  
  
     ![Excel-顯示 MDS 連接詳細資料](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-04.jpg "Excel-顯示 MDS 連接詳細資料")  
  
15. 保持**Excel**開啟。  
  
## <a name="next-task"></a>下一項工作  
 [工作 3：在主資料管理員中驗證資料](../../2014/tutorials/task-3-verifying-the-data-in-master-data-manager.md)  
  
  

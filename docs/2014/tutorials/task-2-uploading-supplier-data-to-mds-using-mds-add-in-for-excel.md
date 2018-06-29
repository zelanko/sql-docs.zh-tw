---
title: 工作 2： 將供應商資料上傳至 MDS 增益集使用適用於 Excel 的 MDS |Microsoft 文件
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
ms.topic: article
ms.assetid: 598deb57-e0cc-4e0a-aeb1-94432c094c67
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 1831fc9ea79027e24d752d05e3b50d3a58d6e06f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36029963"
---
# <a name="task-2-uploading-supplier-data-to-mds-using-mds-add-in-for-excel"></a>工作 2：使用適用於 Excel 的 MDS 增益集將供應商資料上傳到 MDS
  在這項工作，您已清理和供應商將資料發佈至**MDS**使用**MDS 增益集的 Excel**。 建立名為實體**供應商**中**供應商**您在上一課中建立的模型。 此實體將會針對 Excel 檔案中的每個資料行具有一個屬性。 Supplier 實體的 Code 和 Name 屬性對應至**SupplierID**和**Supplier Name**在 Excel 中的資料行。  
  
1.  開啟**清理和比對 Suppliers.xls**中**Excel**。  
  
2.  按**CTRL + A**選取整個資料。 它是**重要**試算表中，選取整個資料。  
  
3.  按一下**主要資料**功能表列上。  
  
4.  按一下**建立實體**功能區上的按鈕。  
  
     ![Excel-主要資料 索引標籤-建立實體 按鈕](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-01.jpg "Excel-主要資料 索引標籤-建立實體 按鈕")  
  
5.  在**管理連接**對話方塊中，如果您看不到連接**本機 MDS 伺服器**下**現有連接**，執行下列動作：  
  
    1.  選取**建立新的連接**，然後按一下**新增** 按鈕。  
  
    2.  在**加入新連接** 對話方塊中，輸入**本機 MDS 伺服器**如**描述**和**http://localhost/MDS**的**MDS 伺服器位址**，然後按一下**確定**以關閉對話方塊。  
  
6.  在**管理連接**對話方塊中，選取**本機 MDS 伺服器**(http://localhost/MDS)，按一下 **測試**來測試連接。 按一下**確定**訊息方塊上。  
  
7.  按一下**連接**連接到 MDS 伺服器。  
  
8.  在**建立實體**對話方塊中，選取**供應商**如**模型**。  
  
9. 請確認**VERSION_1**選取**版本**。  
  
10. 輸入**供應商**如**新實體名稱**。  
  
11. 選取**SupplierID**如**包含唯一識別碼的資料行**欄位 （您也可以產生程式碼自動）。 您基本上對應**SupplierID**中的資料行**Excel**至**程式碼**屬性**供應商**實體。  
  
12. 選取**Supplier Name**如**包含名稱的資料行**欄位。 您基本上對應**Supplier Name**中的資料行**Excel**至**名稱**屬性**供應商**實體。 **程式碼**和**名稱**屬性會強制在 MDS 中實體的屬性。  
  
     ![建立實體 對話方塊](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-02.jpg "建立實體 對話方塊")  
  
13. 按一下**確定**在 MDS 中建立實體，將主要資料發行至實體，並關閉**建立實體** 對話方塊。  
  
14. 現在，您應該會看到標題為新的工作表**供應商**，這是加入至 Excel 試算表，在實體的名稱和工作表頂端您應該會看到工作表連接到 MDS 伺服器。 請注意，原始的工作表 (標題為**Sheet1**) 仍然存在。  
  
     ![Excel-供應商 和 Sheet1 索引標籤](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-03.jpg "Excel-供應商 和 Sheet1 索引標籤")  
  
     ![Excel-顯示 MDS 連接詳細資料](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-04.jpg "Excel-顯示 MDS 連接詳細資料")  
  
15. 保留**Excel**開啟。  
  
## <a name="next-task"></a>下一項工作  
 [工作 3： 確認在主資料管理員的資料](../../2014/tutorials/task-3-verifying-the-data-in-master-data-manager.md)  
  
  
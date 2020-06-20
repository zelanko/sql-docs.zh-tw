---
title: 工作2：使用適用于 Excel 的 MDS 增益集將供應商資料上傳至 MDS |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 598deb57-e0cc-4e0a-aeb1-94432c094c67
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 5e825829eb70b695a619df8caaa59788d0ad413f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85064770"
---
# <a name="task-2-uploading-supplier-data-to-mds-using-mds-add-in-for-excel"></a>工作 2：使用適用於 Excel 的 MDS 增益集將供應商資料上傳到 MDS
  在這項工作中，您會使用**適用于 Excel 的 MDS 增益集**，將清理和供應商資料發行至**mds** 。 您會在上一課建立的**供應商**模型中，建立名為**供應商**的實體。 此實體將會針對 Excel 檔案中的每個資料行具有一個屬性。 [供應商] 實體的 [程式碼] 和 [名稱] 屬性會對應到 Excel 中的 [供貨**商** **] 和 [**  
  
1.  在**Excel**中開啟**清理和相符的 Suppliers.xls** 。  
  
2.  按**CTRL + A**選取整個資料。 請**務必**選取試算表中的完整資料。  
  
3.  按一下功能表列上的 [**主要資料**]。  
  
4.  按一下功能區上的 [**建立實體**] 按鈕。  
  
     ![Excel - [主要資料] 索引標籤 - [建立實體] 按鈕](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-01.jpg "Excel - [主要資料] 索引標籤 - [建立實體] 按鈕")  
  
5.  在 [**管理連接**] 對話方塊中，如果您在 [**現有連接**] 下看不到**本機 MDS 伺服器**的連接，請執行下列動作：  
  
    1.  選取 [**建立新的連接**]，然後按一下 [**新增**] 按鈕。  
  
    2.  在 [**加入新連接**] 對話方塊中，針對 [**描述**] 輸入**本機 Mds 伺服器**，並針對 [ **mds 伺服器位址**] 輸入**HTTP： \/ /localhost/MDS** ，然後按一下 **[確定**] 關閉對話方塊。  
  
6.  在 [**管理連接**] 對話方塊中，選取 [**本機 MDS 伺服器**（ `http://localhost/MDS` ）]，然後按一下 [**測試**] 來測試連接。 在訊息方塊上按一下 **[確定]** 。  
  
7.  按一下 **[連接**]，連接到 MDS 伺服器。  
  
8.  在 [**建立實體**] 對話方塊中，選取 [**供應商**] 做為**模型**。  
  
9. 確定已針對 [**版本**] 選取 [ **VERSION_1** ]。  
  
10. 針對 [**新機構名稱**] 輸入**供應商**。  
  
11. 針對**包含唯一識別碼****欄位的資料**行選取 [中繼資料] （您也可以自動產生程式碼）。 您基本上會將**Excel**中的 [供貨**商**] 資料行對應至 [**供應商**] 實體的 [ **Code** ] 屬性。  
  
12. 針對**包含 [名稱**] 欄位的資料行，選取 [**供應商名稱**]。 您基本上會將**Excel**中的**供應商名稱**資料行對應至**供應商**實體的**name**屬性。 **Code**和**NAME**屬性是 MDS 中實體的必要屬性。  
  
     ![[建立實體] 對話方塊](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-02.jpg "[建立實體] 對話方塊")  
  
13. 按一下 **[確定]** 以在 MDS 上建立實體、將主要資料發行至實體，然後關閉 [**建立實體**] 對話方塊。  
  
14. 現在，您應該會看到標題為「**供應商**」的新工作表，也就是實體的名稱，加入 Excel 試算表，然後在工作表頂端，您應該會看到工作表已連接到 MDS 伺服器。 請注意，原始工作表（標題為**Sheet1**）仍存在。  
  
     ![Excel - [供應商] 和 [Sheet1] 索引標籤](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-03.jpg "Excel - [供應商] 和 [Sheet1] 索引標籤")  
  
     ![Excel - 顯示 MDS 連接詳細資料](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-04.jpg "Excel - 顯示 MDS 連接詳細資料")  
  
15. 讓**Excel**保持開啟。  
  
## <a name="next-task"></a>下一項工作  
 [工作 3：在主資料管理員中驗證資料](../../2014/tutorials/task-3-verifying-the-data-in-master-data-manager.md)  
  
  

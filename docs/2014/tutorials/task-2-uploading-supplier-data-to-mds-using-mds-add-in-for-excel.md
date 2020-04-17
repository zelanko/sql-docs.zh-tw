---
title: 任務 2:使用 Excel 的 MDS 外接程式將供應商數據上載到 MDS |微軟文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 598deb57-e0cc-4e0a-aeb1-94432c094c67
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 4e3cd4cecd88bcad83c6e9f2a59ecd5f225fb02a
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487692"
---
# <a name="task-2-uploading-supplier-data-to-mds-using-mds-add-in-for-excel"></a>工作 2：使用適用於 Excel 的 MDS 增益集將供應商資料上傳到 MDS
  在此任務中,使用 Excel 的**MDS 外接程式**將清理和供應商數據發布到**MDS。** 在上一課中創建的**供應商**模型中創建名為 **「供應商**」的實體。 此實體將會針對 Excel 檔案中的每個資料行具有一個屬性。 供應商實體的代碼和名稱屬性對應於 Excel 中的**供應商 ID**和**供應商名稱**列。  
  
1.  在**Excel**中打開**清潔和匹配供應商.xls。**  
  
2.  按**CTRL+A**選擇整個數據。 請務必選擇**important**電子表格中的整個數據。  
  
3.  按一下選單欄上的 **「主資料**」。  
  
4.  按下功能區上的 **「創建實體」** 按鈕。  
  
     ![Excel - [主要資料] 索引標籤 - [建立實體] 按鈕](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-01.jpg "Excel - [主要資料] 索引標籤 - [建立實體] 按鈕")  
  
5.  在 **「管理連線」** 對話框中,如果在**現有連線**下看不到與**本地 MDS 伺服器**的連線,則執行以下操作:  
  
    1.  選擇 **「建立新連線**」,然後按下 **「新建」** 按鈕。  
  
    2.  在 **「新增新連線**」對話框中,鍵入 **「本地 MDS 伺服器****」 說明「****http:/\/本地主機/MDS MDS 用於****MDS 伺服器位址**」,然後單擊「**確定」** 以關閉該對話框。  
  
6.  在 **「管理連線」** 對話方塊中,選擇 **「本地 MDS 伺服器**」 ()`http://localhost/MDS`「下單擊 **」測試「以**測試連接。 按一下消息框上的 **「確定**」。  
  
7.  按**下連線「** 以連接到 MDS 伺服器。  
  
8.  在 **「建立實體」** 對話框中, 選擇**模型**的**供應商**。  
  
9. 確保為**版本**選擇了**VERSION_1。**  
  
10. 輸入 **「新實體名稱**的**供應商**」。。  
  
11. 為**包含唯一識別子欄位的欄**選擇 **「供應商 ID」。(** 您也可以自動產生代碼)。 您實質上是將**Excel**中的**供應商 ID**列映射到**供應商**實體**的代碼**屬性。  
  
12. 為**包含名稱欄位的列**選擇 **「供應商名稱**」 。 您實質上是將**Excel**中的 **「供應商名稱**」列映射到**供應商**實體**的名稱**屬性。 **代碼**和**名稱**屬性是MDS中實體的必填屬性。  
  
     ![[建立實體] 對話方塊](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-02.jpg "[建立實體] 對話方塊")  
  
13. 按下 **「確定」** 在 MDS 上建立實體,將主資料發布到實體,並關閉 **「創建實體」** 對話框。  
  
14. 現在,您應該看到一個名為 **「供應商**」的新工作表 ,該工作表是實體的名稱,添加到 Excel 電子表格中,在工作表頂部應看到工作表已連接到 MDS 伺服器。 請注意,原始工作表(標題為工作表**1)** 仍然存在。  
  
     ![Excel - [供應商] 和 [Sheet1] 索引標籤](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-03.jpg "Excel - [供應商] 和 [Sheet1] 索引標籤")  
  
     ![Excel - 顯示 MDS 連接詳細資料](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-04.jpg "Excel - 顯示 MDS 連接詳細資料")  
  
15. 保持**Excel**打開。  
  
## <a name="next-task"></a>下一項工作  
 [工作 3：在主資料管理員中驗證資料](../../2014/tutorials/task-3-verifying-the-data-in-master-data-manager.md)  
  
  

---
title: 工作5：從 Excel 建立以網域為基礎的屬性 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 07cbc624-2c6b-4568-96e4-f18663a05d80
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: f7e88065ff66ea953d0a91ed080fc3d7159ab794
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "65489099"
---
# <a name="task-5-creating-a-domain-based-attribute-from-excel"></a>工作 5：從 Excel 建立定義域屬性
  在這項工作中，您會將**供應商**實體的**State**屬性轉換為**網域屬性**。 在您將 State 屬性設定為網域型，並將其發行至 MDS 之後，將會在 MDS 伺服器上建立名為**State**的新實體，其中包含資料行中的所有值，而**供應商**實體的**State**屬性將會填入**State**實體中的值。 現在，**供應商**模型應該有兩個實體 **：供應商和****狀態**，其中**供應商**實體的**State**屬性是相依于**State**實體的網域屬性。  
  
1.  切換至已**清理且符合供應商 .xlsx**的**Excel**視窗。  
  
2.  按一下**功能**區上的 [重新整理] 按鈕，以從 MDS 取得最新的更新。 如果您已執行選用的工作**4**，您應該會看到這兩個記錄。  
  
3.  按一下**標頭資料**列中的 [資料行名稱**狀態**（儲存格**I1**）]。  
  
     ![Excel - [屬性內容] 按鈕](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-01.jpg "Excel - [屬性內容] 按鈕")  
  
4.  按一下功能區上的 [**屬性屬性**]。  
  
5.  在 [**屬性內容] 對話方塊**中，針對 [**屬性類型**] 選取 [**受條件約束的清單（網域型）** ]。  
  
6.  輸入**新機構名稱**的**狀態**，然後按一下 **[確定]**。  
  
     ![Excel - [屬性內容] 對話方塊](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-02.jpg "Excel - [屬性內容] 對話方塊")  
  
7.  現在，在 Excel 中，當您按一下 [ **State** ] 資料行中的任何值時，您應該會看到**向下箭**號。 您可以視需要使用下拉式清單變更此值。  
  
     ![Excel - 含 [美國各州] 的下拉式清單](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-03.jpg "Excel - 含 [美國各州] 的下拉式清單")  
  
## <a name="next-step"></a>後續步驟  
 [工作 6：確認已使用主資料管理員建立定義域屬性](../../2014/tutorials/task-6-verify-domain-based-attribute-master-data-manager.md)  
  
  

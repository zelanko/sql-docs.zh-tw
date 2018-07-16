---
title: 工作 5： 從 Excel 建立的網域屬性 |Microsoft Docs
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
ms.assetid: 07cbc624-2c6b-4568-96e4-f18663a05d80
caps.latest.revision: 6
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8c4b2ae49de561dd7a82785bda955d6701abc770
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37251280"
---
# <a name="task-5-creating-a-domain-based-attribute-from-excel"></a>工作 5：從 Excel 建立定義域屬性
  在這個工作中，您將轉換**狀態**屬性**供應商**實體**網域型屬性**。 設定是以網域為基礎，並將其發行至 MDS，名為的新實體的 State 屬性之後**狀態**資料行中的所有值的 MDS 伺服器上將建立並**狀態**屬性**供應商**的值將會填入實體**狀態**實體。 現在，請**供應商**模型應該有兩個實體：**供應商**並**狀態**其中**狀態**屬性**供應商**實體是取決於網域屬性**狀態**實體。  
  
1.  若要切換**Excel**有視窗**Cleansed and Matched Suppliers.xlsx**開啟。  
  
2.  按一下 **重新整理**從 MDS 取得最新的更新功能區上的按鈕。 如果您已執行選擇性的您應該看到兩筆資料錄**工作 4**。  
  
3.  按一下 資料行名稱**狀態**(資料格**I1**) 中**標頭資料列**。  
  
     ![Excel-[屬性內容] 按鈕](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-01.jpg "Excel-[屬性內容] 按鈕")  
  
4.  按一下  **（Attribute） 屬性**功能區上。  
  
5.  在 **屬性的屬性**對話方塊中，選取**Constrained 清單 （以網域為基礎）** 的**屬性類型**。  
  
6.  型別**狀態**如**新實體名稱**然後按一下**確定**。  
  
     ![Excel-[屬性內容] 對話方塊](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-02.jpg "Excel-[屬性內容] 對話方塊")  
  
7.  現在，在 Excel 中，您應該會看到**向下箭號**當您按一下 使用中的任何值**狀態**資料行。 您可以視需要使用下拉式清單變更此值。  
  
     ![Excel-下拉式清單中具有狀態](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-03.jpg "Excel-下拉式清單中具有狀態")  
  
## <a name="next-step"></a>下一個步驟  
 [工作 6：確認已使用主資料管理員建立定義域屬性](../../2014/tutorials/task-6-verify-domain-based-attribute-master-data-manager.md)  
  
  

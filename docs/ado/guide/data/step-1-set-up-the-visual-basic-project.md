---
title: "步驟 1： 設定 Visual Basic 專案 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 77d3bfa5-fc9f-4a72-93b4-790c7d227988
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8bfdee45f81b2b69e0d495b643878f599345edf5
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="step-1-set-up-the-visual-basic-project"></a>步驟 1： 設定 Visual Basic 專案
在此案例中，假設您有 Microsoft Visual Basic 6.0，ADO 2.5 或更新版本，Microsoft OLE DB Provider for Internet Publishing 安裝在您的系統上。 您將先建立新的專案，並將某些控制項新增到專案中的預設表單。  
  
### <a name="to-create-an-ado-project"></a>若要建立 ADO 專案：  
  
1.  在 Microsoft Visual Basic 中，建立新的標準的 EXE 專案。  
  
2.  從 [專案] 功能表中，選擇 [參考]。  
  
3.  選取 「 Microsoft ActiveX 資料物件 2.5 程式庫 」，然後按一下 [確定]。  
  
### <a name="to-insert-controls-on-the-main-form"></a>若要插入主要表單上的控制項：  
  
1.  將 ListBox 控制項加入至 Form1。 Name 屬性設定為**lstMain**。  
  
2.  將另一個清單方塊控制項加入至 Form1。 Name 屬性設定為**lstDetails**。  
  
3.  將文字方塊控制項加入至 Form1。 Name 屬性設定為**txtDetails**。  
  
## <a name="see-also"></a>請參閱＜  
 [網際網路發佈案例](../../../ado/guide/data/internet-publishing-scenario.md)   
 [步驟 2：初始化 [主要] 清單方塊](../../../ado/guide/data/step-2-initialize-the-main-list-box.md)

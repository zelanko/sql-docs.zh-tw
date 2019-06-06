---
title: 步驟 1:設定 Visual Basic 專案 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 77d3bfa5-fc9f-4a72-93b4-790c7d227988
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b5f6379eb6cfc1d0f9020019d543cda180d9d88b
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66700607"
---
# <a name="step-1-set-up-the-visual-basic-project"></a>步驟 1:設定 Visual Basic 專案
在此案例中，假設您有 Microsoft Visual Basic 6.0 ADO 2.5 或更新版本，Microsoft OLE DB Provider for Internet Publishing 安裝在您的系統上。 您會先建立新的專案，並再將某些控制項新增至專案中的預設表單。  
  
### <a name="to-create-an-ado-project"></a>若要建立 ADO 專案：  
  
1.  在 Microsoft Visual Basic 中，建立新的標準的 EXE 專案。  
  
2.  從 [專案] 功能表中，選擇 [參考]。  
  
3.  選取 「 Microsoft ActiveX 資料物件 2.5 程式庫 」，然後按一下 [確定]。  
  
### <a name="to-insert-controls-on-the-main-form"></a>若要插入主表單上的控制項：  
  
1.  將 ListBox 控制項新增至 Form1。 將其名稱屬性設定為**lstMain**。  
  
2.  將另一個清單方塊控制項新增至 Form1。 將其名稱屬性設定為**lstDetails**。  
  
3.  將文字方塊控制項新增到 Form1。 將其名稱屬性設定為**txtDetails**。  
  
## <a name="see-also"></a>另請參閱  
 [網際網路發佈案例](../../../ado/guide/data/internet-publishing-scenario.md)   
 [步驟 2：初始化 [主要] 清單方塊](../../../ado/guide/data/step-2-initialize-the-main-list-box.md)

---
title: 步驟1：設定 Visual Basic 專案 |Microsoft Docs
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
ms.openlocfilehash: bd44990c38a30f26e682fbb7f1f6aef642043215
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67924077"
---
# <a name="step-1-set-up-the-visual-basic-project"></a>步驟 1：設定 Visual Basic 專案
在此案例中，假設您有 Microsoft Visual Basic 6.0、ADO 2.5 或更新版本，以及您的系統上已安裝網際網路發佈的 Microsoft OLE DB 提供者。 您會先建立新的專案，然後將一些控制項加入至專案中的預設表單。  
  
### <a name="to-create-an-ado-project"></a>若要建立 ADO 專案：  
  
1.  在 Microsoft Visual Basic 中，建立新的標準 EXE 專案。  
  
2.  從 [專案] 功能表中，選擇 [參考]。  
  
3.  選取 [Microsoft ActiveX Data Objects 2.5 程式庫]，然後按一下 [確定]。  
  
### <a name="to-insert-controls-on-the-main-form"></a>若要在主要表單上插入控制項：  
  
1.  將 ListBox 控制項加入至 Form1。 將其 [名稱] 屬性設定為**lstMain**。  
  
2.  將另一個 ListBox 控制項加入 Form1。 將其 [名稱] 屬性設定為**lstDetails**。  
  
3.  將 TextBox 控制項加入 Form1。 將其 [名稱] 屬性設定為**txtDetails**。  
  
## <a name="see-also"></a>另請參閱  
 [網際網路發佈案例](../../../ado/guide/data/internet-publishing-scenario.md)   
 [步驟 2：初始化 [主要] 清單方塊](../../../ado/guide/data/step-2-initialize-the-main-list-box.md)

---
description: 步驟 1：設定 Visual Basic 專案
title: 步驟1：設定 Visual Basic 專案 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 77d3bfa5-fc9f-4a72-93b4-790c7d227988
author: rothja
ms.author: jroth
ms.openlocfilehash: d168a136d4cc80999591f0e36cb65abefa9c6c79
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452810"
---
# <a name="step-1-set-up-the-visual-basic-project"></a>步驟 1：設定 Visual Basic 專案
在此案例中，假設您已在系統上安裝 Microsoft Visual Basic 6.0、ADO 2.5 或更新版本，以及適用于網際網路發佈的 Microsoft OLE DB 提供者。 您將會先建立新的專案，然後將一些控制項加入專案中的預設表單。  
  
### <a name="to-create-an-ado-project"></a>若要建立 ADO 專案：  
  
1.  在 Microsoft Visual Basic 中，建立新的標準 EXE 專案。  
  
2.  從 [專案] 功能表中選擇 [參考]。  
  
3.  選取 [Microsoft ActiveX Data Objects 2.5 程式庫]，然後按一下 [確定]。  
  
### <a name="to-insert-controls-on-the-main-form"></a>若要在主要表單上插入控制項：  
  
1.  將 ListBox 控制項新增至 Form1。 將其 [名稱] 屬性設定為 [ **lstMain**]。  
  
2.  將另一個 ListBox 控制項新增至 Form1。 將其 [名稱] 屬性設定為 [ **lstDetails**]。  
  
3.  將 TextBox 控制項新增至 Form1。 將其 [名稱] 屬性設定為 [ **txtDetails**]。  
  
## <a name="see-also"></a>另請參閱  
 [網際網路發佈案例](../../../ado/guide/data/internet-publishing-scenario.md)   
 [步驟 2：初始化 [主要] 清單方塊](../../../ado/guide/data/step-2-initialize-the-main-list-box.md)

---
title: "自訂報表項目架構 |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom report items, architecture
ms.assetid: 2a88ea46-c9f8-4dd7-aad1-16de11da4f06
caps.latest.revision: 16
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 8b79071c67e3ada6fcfc0f588d9cba4580a981e8
ms.contentlocale: zh-tw
ms.lasthandoff: 06/13/2017

---
# <a name="custom-report-item-architecture"></a>自訂報表項目架構
  自訂報表項目是報表定義語言 (RDL) 的延伸模組，可讓開發人員加入 RDL 中原本就支援的功能，或是擴充現有控制項的功能。 自訂報表項目有兩個主要元件：執行階段元件與設計階段元件。 這些元件會實作成 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 組件，而且可用任何 CLS 相容的語言來撰寫。  
  
## <a name="the-run-time-component"></a>執行階段元件  
 自訂報表項目的執行階段元件會在執行階段由報表處理器進行呼叫。 執行階段元件會接受報表處理器在執行階段所傳遞的資料、處理這個資料，並傳回包含已轉譯之自訂報表項目的影像。  
  
 ![自訂報表項目執行階段元件](../../reporting-services/custom-report-items/media/customreportitemrun-timecomponentarchitecture.gif "自訂報表項目執行階段元件")  
  
## <a name="the-design-time-component"></a>設計階段元件  
 設計階段元件允許在 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 的報表設計師介面中定義和操作自訂報表項目。 設計階段元件是由幾個子控制項所組成，這些子控制項可控制設計環境中自訂報表項目的外觀與屬性。  
  
 ![自訂報表項目設計階段元件](../../reporting-services/custom-report-items/media/customreportitemdesign-timecomponentarchitecture.gif "自訂報表項目設計階段元件")  
  
## <a name="see-also"></a>另請參閱  
 [建立自訂報表項目執行階段元件](../../reporting-services/custom-report-items/creating-a-custom-report-item-run-time-component.md)   
 [建立自訂報表項目設計階段元件](../../reporting-services/custom-report-items/creating-a-custom-report-item-design-time-component.md)   
 [如何： 部署自訂報表項目](../../reporting-services/custom-report-items/how-to-deploy-a-custom-report-item.md)  
  
  

---
title: 自訂報表項目架構 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- custom report items, architecture
ms.assetid: 2a88ea46-c9f8-4dd7-aad1-16de11da4f06
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a053eb55547da9030eebe9036667cca2e14606f1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63264944"
---
# <a name="custom-report-item-architecture"></a>自訂報表項目架構
  自訂報表項目是報表定義語言 (RDL) 的延伸模組，可讓開發人員新增 RDL 中原本就支援的功能，或是擴充現有控制項的功能。 自訂報表項目有兩個主要元件：執行階段元件與設計階段元件。 這些元件會實作成 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 組件，而且可用任何 符合 CLS 規範的語言來撰寫。  
  
## <a name="the-run-time-component"></a>執行階段元件  
 自訂報表項目的執行階段元件會在執行階段由報表處理器進行呼叫。 執行階段元件會接受報表處理器在執行階段所傳遞的資料、處理這個資料，並傳回包含已轉譯之自訂報表項目的影像。  
  
 ![自訂報表項目執行階段元件](../../../2014/reporting-services/media/customreportitemrun-timecomponentarchitecture.gif "自訂報表項目執行階段元件")  
  
## <a name="the-design-time-component"></a>設計階段元件  
 設計階段元件允許在 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 的報表設計師介面中定義和操作自訂報表項目。 設計階段元件是由幾個子控制項所組成，這些子控制項可控制設計環境中自訂報表項目的外觀與屬性。  
  
 ![自訂報表項目設計階段元件](../../../2014/reporting-services/media/customreportitemdesign-timecomponentarchitecture.gif "自訂報表項目設計階段元件")  
  
## <a name="see-also"></a>另請參閱  
 [建立自訂報表項目執行階段元件](../custom-report-items/creating-a-custom-report-item-run-time-component.md)   
 [建立自訂報表專案設計階段元件](../custom-report-items/creating-a-custom-report-item-design-time-component.md)   
 [如何：部署自訂報表項目](../custom-report-items/how-to-deploy-a-custom-report-item.md)  
  
  

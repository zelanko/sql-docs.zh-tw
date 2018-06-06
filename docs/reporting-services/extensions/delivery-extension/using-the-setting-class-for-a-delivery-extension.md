---
title: 使用傳遞延伸模組的設定類別 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: extensions
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- delivery extensions [Reporting Services], settings
- Setting class
ms.assetid: 50746639-da7c-46a5-ac7b-e87dd6b91880
caps.latest.revision: 32
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 5d74af9c4f9c1b5f9ddfd1504ad200f5d6ffa49b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="using-the-setting-class-for-a-delivery-extension"></a>使用傳遞延伸模組的設定類別
  <xref:Microsoft.ReportingServices.Interfaces.Setting> 類別是位在 <xref:Microsoft.ReportingServices.Interfaces> 命名空間中，並且代表有關傳遞延伸模組的延伸模組設定。 <xref:Microsoft.ReportingServices.Interfaces.Setting> 類別提供基礎結構，以儲存有關為了使傳遞延伸模組正常運作所需的設定。 例如，「報表伺服器電子郵件」傳遞，使用者需要提供電子郵件傳遞特有的設定，例如收件者地址、寄件者地址、電子郵件的主旨等等。 毋庸置疑地，您的自訂傳遞提供者將要求使用者提供特定的設定，傳遞延伸模組才能傳遞通知和報表。  
  
 當實作 <xref:Microsoft.ReportingServices.Interfaces.Setting> 介面的 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ExtensionSettings%2A> 屬性時，會使用 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension> 類別。 <xref:Microsoft.ReportingServices.Interfaces.Setting> 類別也可在建立訂閱或通知時，用來處理使用者提供的延伸模組設定資料。  
  
 如需如何使用 <xref:Microsoft.ReportingServices.Interfaces.Setting> 類別的範例，請參閱 [SQL Server Reporting Services Product Samples](http://go.microsoft.com/fwlink/?LinkId=177889) (SQL Server Reporting Services 產品範例)。  
  
## <a name="see-also"></a>另請參閱  
 [實作傳遞延伸模組](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services 延伸模組程式庫](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  

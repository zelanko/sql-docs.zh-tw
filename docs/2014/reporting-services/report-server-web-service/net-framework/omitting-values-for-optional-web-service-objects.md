---
title: 省略選擇性 Web 服務物件的值 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- Web service [Reporting Services], omitted values
- XML Web service [Reporting Services], omitted values
- Report Server Web service, omitted values
- omitting values [Reporting Services]
ms.assetid: ceb68b8b-9214-4745-abc9-f47f33ecd6f7
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3858f73e1b332acfa1a1bbc640007f6f0884abff
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63260705"
---
# <a name="omitting-values-for-optional-web-service-objects"></a>省略選擇性 Web 服務物件的值
  數個報表伺服器 Web 服務複雜類型的屬性具有隨附的屬性，稱為指定的屬性。 屬性的名稱是由原始的屬性名稱所組成，此名稱中附加了 "Specified" 這個字。 此屬性的存在表示有時可能會省略原始屬性的值。 這是從 Web 服務描述語言 (WSDL) 翻譯為 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] Proxy 類別的直接結果。 例如，複雜類型 <xref:ReportService2010.DataSourceDefinition.Enabled%2A> 的 Web 服務屬性 <xref:ReportService2010.DataSourceDefinition> 具有名為 <xref:ReportService2010.DataSourceDefinition.EnabledSpecified%2A> 的隨附屬性。 如果您要建立應用程式而不想設定 <xref:ReportService2010.DataSourceDefinition.Enabled%2A> 屬性的值，您不需要提供 <xref:ReportService2010.DataSourceDefinition.Enabled%2A> 的值；系統會使用 `true` 預設值。 不過，您仍需要將 <xref:ReportService2010.DataSourceDefinition.EnabledSpecified%2A> 設定為 `false`。 如果您為 <xref:ReportService2010.DataSourceDefinition.Enabled%2A> 屬性提供值，則需要將 <xref:ReportService2010.DataSourceDefinition.EnabledSpecified%2A> 設定為等於 `true`。 這是針對可寫入屬性的情況。 如果是唯讀屬性，則不需要採取任何動作。  
  
> [!IMPORTANT]  
>  如果無法使用上述的技術指定屬性，就可能導致無法預測的 Web 服務行為。  
  
 通常需要您處理其他指定屬性的資料類型包括`Boolean`， `DateTime`，和`Enumeration`。  
  
 如需範例，請參閱 <xref:ReportService2010.ReportingService2010.CreateDataSource%2A> 方法。  
  
## <a name="see-also"></a>另請參閱  
 [使用 Web 服務和 .NET Framework 建置應用程式](building-applications-using-the-web-service-and-the-net-framework.md)   
 [技術參考 &#40;SSRS&#41;](../../technical-reference-ssrs.md)  
  
  

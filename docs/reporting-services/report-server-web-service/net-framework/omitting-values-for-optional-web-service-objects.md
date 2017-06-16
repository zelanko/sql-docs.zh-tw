---
title: "省略選擇性 Web 服務物件的值 |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
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
- Web service [Reporting Services], omitted values
- XML Web service [Reporting Services], omitted values
- Report Server Web service, omitted values
- omitting values [Reporting Services]
ms.assetid: ceb68b8b-9214-4745-abc9-f47f33ecd6f7
caps.latest.revision: 36
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 890b0d174e5277f45db91db23725ae203edf4e2f
ms.contentlocale: zh-tw
ms.lasthandoff: 06/13/2017

---
# <a name="omitting-values-for-optional-web-service-objects"></a>省略選擇性 Web 服務物件的值
  數個報表伺服器 Web 服務複雜類型的屬性具有隨附稱為指定屬性的屬性。 屬性的名稱是由原始的屬性名稱所組成，此名稱中附加了 "Specified" 這個字。 此屬性的存在表示有時可能會省略原始屬性的值。 這是從 Web 服務描述語言 (WSDL) 翻譯為 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] Proxy 類別的直接結果。 例如，複雜類型 <xref:ReportService2010.DataSourceDefinition.Enabled%2A> 的 Web 服務屬性 <xref:ReportService2010.DataSourceDefinition> 具有名為 <xref:ReportService2010.DataSourceDefinition.EnabledSpecified%2A> 的隨附屬性。 如果您要建置的應用程式，而且不想要設定的值<xref:ReportService2010.DataSourceDefinition.Enabled%2A>屬性，您不必提供的值<xref:ReportService2010.DataSourceDefinition.Enabled%2A>; 預設值的**true**用。 不過，您仍需要設定<xref:ReportService2010.DataSourceDefinition.EnabledSpecified%2A>至**false**。 如果您提供的值<xref:ReportService2010.DataSourceDefinition.Enabled%2A>屬性，您需要設定<xref:ReportService2010.DataSourceDefinition.EnabledSpecified%2A>等於**true**。 這是針對可寫入屬性的情況。 如果是唯讀屬性，則不需要採取任何動作。  
  
> [!IMPORTANT]  
>  如果無法使用上述的技術指定屬性，就可能導致無法預測的 Web 服務行為。  
  
 通常需要您處理其他的指定屬性的資料類型包括**布林**， **DateTime**，和**列舉**。  
  
 如需範例，請參閱 <xref:ReportService2010.ReportingService2010.CreateDataSource%2A> 方法。  
  
## <a name="see-also"></a>另請參閱  
 [使用 Web 服務和.NET Framework 建置應用程式](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [技術參考 &#40;SSRS&#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  

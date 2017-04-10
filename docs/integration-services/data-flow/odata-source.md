---
title: "OData 來源 | Microsoft Docs"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.DTS.DESIGNER.ODATASOURCE.F1"
ms.assetid: cc9003c9-638e-432b-867e-e949d50cec90
caps.latest.revision: 14
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 14
---
# OData 來源
  使用 SSIS 封裝中的 OData 來源元件，從開放式資料通訊協定 (OData) 服務取用資料。 此元件支援 OData v3 和 v4 通訊協定。  
  
-   針對 OData V3 通訊協定，此元件支援 ATOM 和 JSON 資料格式。  
  
-   針對 OData V4 通訊協定，此元件支援 JSON 資料格式。  
  
> [!NOTE]  
>  您也可以使用 OData 來源，從 SharePoint 清單讀取。 若要查看 SharePoint 伺服器上的所有清單，請使用下列 URL：http://\<伺服器>/_vti_bin/ListData.svc。 如需 SharePoint URL 慣例的詳細資訊，請參閱 [SharePoint Foundation REST 介面](http://msdn.microsoft.com/library/ff521587.aspx)。  OData 來源現在支援 Microsoft Dynamics AX Online 和 Microsoft Dynamics CRM Online 產品。
  
## <a name="odata-format"></a>OData 格式  
 大部分的 OData 服務都會傳回多種格式的結果。 您可使用 $format 查詢選項來指定結果集的格式。 類似 JSON 和 JSON Light 的格式要比 ATOM 或 XML 更有效率，而且在傳輸大量資料時可能會提供更好的效能。 下表提供範例測試的結果。 如您所見，當從 ATOM 切換到 JSON 時有 30-53% 的效能提升，而且當從 ATOM 切換到新的 JSON light 格式時有 67% 的效能提升 (適用於 WCF Data Services 5.1)。  
  
|||||  
|-|-|-|-|  
|資料列|ATOM|JSON|JSON (Light)|  
|10000|113 秒|74 秒|68 秒|  
|1000000|1110 秒|853 秒|665 秒|  
  
> [!NOTE]  
>  SSIS OData 來源會使用 5.6.1 來剖析 OData V3 摘要，使用 ODataLib 6.12.0 來剖析 OData V4 摘要。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [教學課程：使用 OData 來源](../../integration-services/data-flow/tutorial-using-the-odata-source.md)  
  
-   [在執行階段修改 OData 來源查詢](../../integration-services/data-flow/modify-odata-source-query-at-runtime.md)  
  
-   [OData 來源編輯器 &#40;[連線] 頁面&#41;](../Topic/OData%20Source%20Editor%20\(Connection%20Page\).md)  
  
-   [OData 來源編輯器 &#40;[資料行] 頁面&#41;](../Topic/OData%20Source%20Editor%20\(Columns%20Page\).md)  
  
-   [OData 來源編輯器 &#40;[錯誤輸出] 頁面&#41;](../Topic/OData%20Source%20Editor%20\(Error%20Output%20Page\).md)  
  
-   [OData 來源屬性](../../integration-services/data-flow/odata-source-properties.md)  
  
## <a name="see-also"></a>另請參閱  
 [OData 連線管理員](../../integration-services/connection-manager/odata-connection-manager.md)  
  
  
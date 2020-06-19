---
title: OData 來源 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.DTS.DESIGNER.ODATASOURCE.F1
ms.assetid: cc9003c9-638e-432b-867e-e949d50cec90
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 0504d7be4060afc9c46a46fa3968523537381882
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84915158"
---
# <a name="odata-source"></a>OData 來源
  您可使用 SSIS 封裝中的 OData 來源元件，從開放式資料通訊協定 (OData) 服務取用資料。 此元件支援 OData v2 和 v3 通訊協定以及 ATOM 和 JSON 資料格式。  
  
> [!NOTE]  
>  OData 來源可用來從 SharePoint 清單讀取。 若要查看 SharePoint 伺服器上的所有清單，請使用下列 URL： HTTP:// \<server> /_vti_bin/listdata.svc。 如需 SharePoint URL 慣例的詳細資訊，請參閱 [SharePoint Foundation REST 介面](https://msdn.microsoft.com/library/ff521587.aspx)。  
  
## <a name="odata-format"></a>OData 格式  
 大部分的 OData 服務都會傳回多種格式的結果。 您可使用 $format 查詢選項來指定結果集的格式。 類似 JSON 和 JSON Light 的格式要比 ATOM/XML 更有效率，而且在傳輸大量資料時可能會提供更好的效能。 下表提供範例測試的結果。 如您所見，當從 ATOM 切換到 JSON 時有 30-53% 的效能提升，而且當從 ATOM 切換到新的 JSON light 格式時有 67% 的效能提升 (適用於 WCF Data Services 5.1)。  
  
|||||  
|-|-|-|-|  
|資料列|ATOM|JSON|JSON (Light)|  
|10000|113 秒|74 秒|68 秒|  
|1000000|1110 秒|853 秒|665 秒|  
  
> [!NOTE]  
>  SSIS OData 來源會使用 ODataLib 5.5.0 來剖析 OData 摘要，而且它可以讀取此程式庫所支援的所有格式。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [安裝及解除安裝 OData 來源元件](../install-and-uninstall-odata-source-component.md)  
  
-   [教學課程：使用 &#91;SSIS 的 OData 來源&#93;](tutorial-using-the-odata-source.md)  
  
-   [在執行階段修改 OData 來源查詢](modify-odata-source-query-at-runtime.md)  
  
-   [OData 來源編輯器 &#40;[連線] 頁面&#41;](../odata-source-editor-connection-page.md)  
  
-   [OData 來源編輯器 &#40;資料行頁面&#41;](../odata-source-editor-columns-page.md)  
  
-   [OData 來源編輯器 &#40;[錯誤輸出] 頁面&#41;](../odata-source-editor-error-output-page.md)  
  
-   [OData 來源屬性](odata-source-properties.md)  
  
## <a name="see-also"></a>另請參閱  
 [OData 連接管理員](../connection-manager/odata-connection-manager.md)  
  
  

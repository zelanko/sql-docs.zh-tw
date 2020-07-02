---
title: 自動建立代碼
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 9adbd5e1-f28c-4fb5-afa7-082de2831f3e
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 057162b74045ac32a8f4504496417f274a02b423
ms.sourcegitcommit: 6be9a0ff0717f412ece7f8ede07ef01f66ea2061
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85812044"
---
# <a name="automatic-code-creation-master-data-services"></a>自動建立代碼 (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，您可以針對 Code 屬性，或針對其他任何數值屬性，自動產生數值。 自動產生代碼時，系統不會防止您針對代碼輸入其他值，但是會自動設定初始值。  
  
## <a name="generating-code-values"></a>產生代碼值  
 管理員可以編輯相關實體的屬性，藉以設定 Code 屬性的自動產生值。 他們可以指定一個初始值，而且每個後續的值以一遞增。  
  
 當您使用其中一種工具或暫存處理序，將 Code 值輸入至 MDS 時，可以將 Code 值留空，就會自動產生 Code 值。 或者，您也可以指定自己選擇的 Code 值。  
  
## <a name="generating-other-attribute-values"></a>產生其他屬性值  
 管理員可以透過建立商務規則，為 Code 以外的其他屬性自動產生值。 他們可以指定一個初始值，而且可以指定每個後續值的遞增數目。  
  
 當您使用其中一種工具或暫存處理序，將屬性值輸入至 MDS 時，可以將屬性值留空。 套用商務規則時，將會根據最高的現有值遞增這些值。 例如，如果您的規則是「將屬性預設為從 1 開始產生，並以 4 遞增的值」，而且該屬性最高的目前值為 700，則新增之下一個成員的值將是 704。  
  
## <a name="related-tasks"></a>相關工作  
  
|工作描述|主題|  
|----------------------|-----------|  
|自動為 Code 屬性產生值。|[自動產生 Code 屬性值 &#40;Master Data Services&#41;](../master-data-services/automatically-generate-code-attribute-values-master-data-services.md)|  
|自動為其他屬性產生值。|[自動產生 Code 以外的屬性值 &#40;Master Data Services&#41;](../master-data-services/automatically-generate-attribute-values-other-than-code-master-data-services.md)|  
  
## <a name="related-content"></a>相關內容  
  
-   [Master Data Services 概觀 &#40;MDS&#41;](../master-data-services/master-data-services-overview-mds.md)  
  
-   [商務規則 &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)  
  
-   [實體 &#40;Master Data Services&#41;](../master-data-services/entities-master-data-services.md)  
  
  

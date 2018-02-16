---
title: "層級內容-使用者階層 |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- user hierarchies [Analysis Services]
- hierarchies [Analysis Services], user
ms.assetid: dabb7335-887b-442a-b67c-4901ba1242b7
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: db94622cfc84d97cb6f8e7578421f4933a63af94
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2018
---
# <a name="user-hierarchies---level-properties"></a>使用者階層的層級屬性
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
下表列出並描述使用者自訂階層中的層級屬性。  
  
|屬性|Description|  
|--------------|-----------------|  
|Description|包含層級的描述。|  
|HideMemberIf|指出是否應向用戶端應用程式隱藏層級中的成員，以及何時隱藏。 此屬性可以有下列的值：<br /><br /> 永不<br /> 永不隱藏成員。 這是預設值。<br /><br /> OnlyChildWithNoName<br /> 當成員是其父系的唯一子系，且成員的名稱為空白時，就會隱藏成員。<br /><br /> OnlyChildWithParentName<br /> 當成員是其父系的唯一子系，且成員與其父系有相同的名稱時，就會隱藏成員。<br /><br /> NoName<br /> 當成員的名稱為空白時，就會隱藏成員。<br /><br /> ParentName<br /> 當成員與其父系有相同的名稱時，就會隱藏成員。|  
|ID|包含層級的唯一識別碼 (ID)。|  
|名稱|包含層級的易記名稱。 依預設，層級與來源屬性有相同的名稱。|  
|SourceAttribute|包含作為層級基礎之來源屬性的名稱。|  
  
## <a name="see-also"></a>另請參閱  
 [使用者階層屬性](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md)  
  
  

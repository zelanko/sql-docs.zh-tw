---
title: 層級屬性 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- user hierarchies [Analysis Services]
- hierarchies [Analysis Services], user
ms.assetid: dabb7335-887b-442a-b67c-4901ba1242b7
author: minewiskan
ms.author: owend
ms.openlocfilehash: 553503b9d35142bcc998b4ec12ad2e29d4c66318
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84545070"
---
# <a name="level-properties"></a>層級屬性 
  下表列出並描述使用者自訂階層中的層級屬性。  
  
|屬性|描述|  
|--------------|-----------------|  
|Description|包含層級的描述。|  
|HideMemberIf|指出是否應向用戶端應用程式隱藏層級中的成員，以及何時隱藏。 此屬性可以有下列的值：<br /><br /> 永不<br /> 永不隱藏成員。 這是預設值。<br /><br /> OnlyChildWithNoName<br /> 當成員是其父系的唯一子系，且成員的名稱為空白時，就會隱藏成員。<br /><br /> OnlyChildWithParentName<br /> 當成員是其父系的唯一子系，且成員與其父系有相同的名稱時，就會隱藏成員。<br /><br /> NoName<br /> 當成員的名稱為空白時，就會隱藏成員。<br /><br /> ParentName<br /> 當成員與其父系有相同的名稱時，就會隱藏成員。|  
|ID|包含層級的唯一識別碼 (ID)。|  
|Name|包含層級的易記名稱。 依預設，層級與來源屬性有相同的名稱。|  
|SourceAttribute|包含作為層級基礎之來源屬性的名稱。|  
  
## <a name="see-also"></a>另請參閱  
 [使用者階層屬性](user-hierarchies-properties.md)  
  
  

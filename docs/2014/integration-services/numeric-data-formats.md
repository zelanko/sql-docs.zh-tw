---
title: 數值資料格式 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- integer data types [Integration Services]
- numeric data formats for fast parse
- locale-sensitive parsing [Integration Services]
- fast parse [Integration Services]
ms.assetid: fa3975ce-9d21-408a-857d-f85e30af27b0
caps.latest.revision: 33
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1ed822a26c5722a249c3fda635288c282f3e2834
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37180285"
---
# <a name="numeric-data-formats"></a>數值資料格式
  快速剖析提供一組快速、簡易且區分區域設定的常式集，以剖析資料。 快速剖析僅支援整數資料類型的有限格式集。  
  
## <a name="integer-data-types"></a>整數資料類型  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 所提供的整數資料類型為 DT_I1、DT_UI1、DT_I2、DT_UI2、DT_I4、DT_UI4、DT_I8 及 DT_UI8。 如需詳細資訊，請參閱 [Integration Services 資料類型](data-flow/integration-services-data-types.md)。  
  
 快速剖析支援整數資料類型的下列格式：  
  
-   含或不含開頭與尾端空格或定位點。 例如，值「  123  」為有效。 全部為空格的值會評估為零。  
  
-   開頭正號、負號或均不含。 例如，值 +123、-123 及 123 有效。  
  
-   一個或多個印度-阿拉伯數字 (0-9)。 例如，值 345 有效。 不支援其他語言的數字。  
  
 不支援的資料格式包括：  
  
-   特殊字元。 例如，不支援貨幣字元 $，因此無法剖析值 $20。  
  
-   空白字元，如換行字元、歸位字元及不中斷空格。 例如，無法剖析值「&#xA0;</ph>123」。  
  
-   整數的十六進位表示法。 例如，無法剖析值 2EE。  
  
-   整數的科學記號標記法。 例如，無法剖析值 1E+10。  
  
 下列格式是整數的輸出資料格式：  
  
-   減號代表負數，不含符號則代表正數。  
  
-   無空白。  
  
-   一個或多個印度-阿拉伯數字 (0-9)。  
  
  

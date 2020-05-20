---
title: XML 中的記錄集動態屬性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset dynamic properties in XML [ADO]
ms.assetid: 52f8e379-812a-4db8-9210-94458926301c
author: rothja
ms.author: jroth
ms.openlocfilehash: d9d19ded093cd10a7670b31cd2d5c78a475950d2
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760964"
---
# <a name="recordset-dynamic-properties-in-xml"></a>XML 中的資料錄集動態屬性
下列記錄集提供者特定的屬性（來自用戶端資料指標引擎）目前會保存為 XML 格式：  
  
-   更新重新同步  
  
-   Unique Table  
  
-   唯一的架構  
  
-   唯一目錄  
  
-   重新同步命令  
  
-   IRowsetChange  
  
-   IRowsetUpdate  
  
-   CommandTimeout  
  
-   BatchSize  
  
-   UpdateCriteria  
  
-   重新調整名稱  
  
-   AutoRecalc  
  
 這些屬性會儲存在架構區段中，做為要保存之記錄集的元素定義屬性。 這些屬性是在資料列集架構命名空間中定義，而且必須具有前置詞 "rs："。  
  
## <a name="see-also"></a>另請參閱  
 [以 XML 格式保存記錄](../../../ado/guide/data/persisting-records-in-xml-format.md)

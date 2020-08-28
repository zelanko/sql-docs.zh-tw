---
description: XML 中的資料錄集動態屬性
title: XML 中的記錄集動態屬性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset dynamic properties in XML [ADO]
ms.assetid: 52f8e379-812a-4db8-9210-94458926301c
author: rothja
ms.author: jroth
ms.openlocfilehash: 395a81108e3ceaed99ad8ccf1fbab29831dd116d
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979889"
---
# <a name="recordset-dynamic-properties-in-xml"></a>XML 中的資料錄集動態屬性
下列記錄集提供者特定屬性 (自用戶端資料指標引擎) 目前保存為 XML 格式：  
  
-   更新重新同步  
  
-   Unique Table  
  
-   唯一架構  
  
-   唯一目錄  
  
-   Resync 命令  
  
-   IRowsetChange  
  
-   IRowsetUpdate  
  
-   CommandTimeout  
  
-   BatchSize  
  
-   UpdateCriteria  
  
-   重新調整名稱  
  
-   AutoRecalc  
  
 這些屬性會儲存在 [架構] 區段中，做為要保存之記錄集的元素定義屬性。 這些屬性是在資料列集架構命名空間中定義，而且必須有前置詞 "rs："。  
  
## <a name="see-also"></a>另請參閱  
 [以 XML 格式保存記錄](../../../ado/guide/data/persisting-records-in-xml-format.md)

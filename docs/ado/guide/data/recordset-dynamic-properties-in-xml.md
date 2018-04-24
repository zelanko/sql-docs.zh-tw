---
title: 在 XML 中的資料錄集的動態屬性 |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset dynamic properties in XML [ADO]
ms.assetid: 52f8e379-812a-4db8-9210-94458926301c
caps.latest.revision: 3
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1ad6aae69440da01f2a18ec474a0a2af63465ad7
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2018
---
# <a name="recordset-dynamic-properties-in-xml"></a>在 XML 中的資料錄集的動態內容
下列的資料錄集提供者特定屬性 （從用戶端資料指標引擎） 目前會保存為 XML 格式：  
  
-   更新的重新同步處理  
  
-   唯一資料表  
  
-   唯一的結構描述  
  
-   唯一的目錄  
  
-   重新同步處理命令  
  
-   IRowsetChange  
  
-   IRowsetUpdate  
  
-   CommandTimeout  
  
-   BatchSize  
  
-   UpdateCriteria  
  
-   重繪名稱  
  
-   AutoRecalc  
  
 這些屬性會儲存在結構描述 」 一節，以保存資料錄集的項目定義的屬性。 這些屬性定義在資料列集結構描述命名空間，而且必須有前置詞"rs:"。  
  
## <a name="see-also"></a>另請參閱  
 [以 XML 格式保存記錄](../../../ado/guide/data/persisting-records-in-xml-format.md)

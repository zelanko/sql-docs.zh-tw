---
description: DataMember 屬性
title: DataMember 屬性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::DataMember
helpviewer_keywords:
- DataMember property
ms.assetid: 2c8fb09e-10ad-49b5-ab41-2603771780d9
author: rothja
ms.author: jroth
ms.openlocfilehash: f698c4a20fb76839460ca0930d45b8d18b2738be
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444230"
---
# <a name="datamember-property"></a>DataMember 屬性
指出將從[DataSource](../../../ado/reference/ado-api/datasource-property-ado.md)屬性所參考的[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)取出的資料成員名稱。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回 **字串** 值。 名稱不區分大小寫。  
  
## <a name="remarks"></a>備註  
 這個屬性是用來建立資料繫結控制項與資料環境。 資料環境會維護資料 (資料來源的集合，) 包含命名物件 (資料成員) 將表示為 [記錄集](../../../ado/reference/ado-api/recordset-object-ado.md) 物件。  
  
 **DataMember**和**DataSource**屬性必須一起使用。  
  
 **DataMember**屬性會決定**DataSource**屬性所指定的物件將會表示為**記錄集**物件。 必須先關閉 **記錄集** 物件，才能設定此屬性。 如果**datasource**屬性之前未設定**datamember**屬性，或**datasource**屬性中指定的物件無法辨識**datamember**名稱，就會產生錯誤。  
  
## <a name="usage"></a>使用量  
  
```  
Dim rs as New ADODB.Recordset  
rs.DataMember = "Command"     'Name of the rowset to bind to  
Set rs.DataSource = myDE      'Name of the object containing an IRowset  
```  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [DataSource 屬性 (ADO)](../../../ado/reference/ado-api/datasource-property-ado.md)

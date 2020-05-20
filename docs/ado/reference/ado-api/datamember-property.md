---
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
ms.openlocfilehash: 87d525907edde2e3dc99b78eb827c571c604d8b7
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763479"
---
# <a name="datamember-property"></a>DataMember 屬性
指出將從[DataSource](../../../ado/reference/ado-api/datasource-property-ado.md)屬性所參考之[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)抓取的資料成員名稱。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**字串**值。 名稱不區分大小寫。  
  
## <a name="remarks"></a>備註  
 這個屬性是用來建立資料繫結控制項與資料環境。 資料環境會維護資料（資料來源）集合，其中包含將表示為[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件的已命名物件（資料成員）。  
  
 **DataMember**和**DataSource**屬性必須一起使用。  
  
 **DataMember**屬性會判斷**DataSource**屬性所指定的物件將會表示為**記錄集**物件。 設定此屬性之前，必須先關閉**記錄集**物件。 如果**datamember**屬性未設定于**datasource**屬性之前，或**datasource**屬性中指定的物件無法辨識**datamember**名稱，則會產生錯誤。  
  
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

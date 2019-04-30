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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b7a1bb2d55fbf4e8d2030c612a1d000b93ca1110
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63308740"
---
# <a name="datamember-property"></a>DataMember 屬性
表示將會從擷取的資料成員名稱[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)所參考[DataSource](../../../ado/reference/ado-api/datasource-property-ado.md)屬性。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**字串**值。 名稱不區分大小寫。  
  
## <a name="remarks"></a>備註  
 這個屬性用來與資料環境中建立資料繫結控制項。 資料環境維護集合包含的資料 （資料來源） 為具名物件 （資料成員），將會呈現為[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件。  
  
 **DataMember**並**DataSource**屬性必須一起使用。  
  
 **DataMember**屬性會決定所指定的物件**DataSource**屬性會表示成**資料錄集**物件。 **資料錄集**必須先關閉物件，這個屬性設定。 如果會產生錯誤**DataMember**屬性未設定之前**DataSource**屬性，或如果**DataMember**名稱無法辨識指定的物件**DataSource**屬性。  
  
## <a name="usage"></a>使用量  
  
```  
Dim rs as New ADODB.Recordset  
rs.DataMember = "Command"     'Name of the rowset to bind to  
Set rs.DataSource = myDE      'Name of the object containing an IRowset  
```  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [DataSource 屬性 (ADO)](../../../ado/reference/ado-api/datasource-property-ado.md)

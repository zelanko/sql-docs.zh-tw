---
title: DataMember 屬性 |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::DataMember
helpviewer_keywords:
- DataMember property
ms.assetid: 2c8fb09e-10ad-49b5-ab41-2603771780d9
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d194cea2dd1a7bbabf8acd2e9d89945772eddd31
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35277407"
---
# <a name="datamember-property"></a>DataMember 屬性
表示將會從擷取的資料成員名稱[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)所參考[DataSource](../../../ado/reference/ado-api/datasource-property-ado.md)屬性。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**字串**值。 名稱不區分大小寫。  
  
## <a name="remarks"></a>備註  
 這個屬性用來建立資料繫結控制項與資料環境。 資料環境會維護資料 （資料來源） 包含集合的具名物件 （資料成員），將會表示為[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件。  
  
 **DataMember**和**DataSource**屬性必須同時使用。  
  
 **DataMember**屬性會決定哪一個物件所指定**DataSource**屬性會表示為**資料錄集**物件。 **資料錄集**必須先關閉物件，這個屬性設定。 如果會產生錯誤**DataMember**屬性未設定之前**DataSource**屬性，或如果**DataMember**名稱無法辨識指定的物件**DataSource**屬性。  
  
## <a name="usage"></a>使用方式  
  
```  
Dim rs as New ADODB.Recordset  
rs.DataMember = "Command"     'Name of the rowset to bind to  
Set rs.DataSource = myDE      'Name of the object containing an IRowset  
```  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [DataSource 屬性 (ADO)](../../../ado/reference/ado-api/datasource-property-ado.md)

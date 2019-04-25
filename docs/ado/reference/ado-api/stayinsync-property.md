---
title: StayInSync 屬性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::StayInSync
- Recordset20::put_StayInSync
- Recordset20::PutStayInSync
- Recordset20::get_StayInSync
- Recordset20::GetStayInSync
helpviewer_keywords:
- StayInSync property
ms.assetid: 502d69b5-dc9a-455d-b115-a03bd39a552b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 50cf569f6e0af5e753cca7fba030b8fc2caa4a86
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62743124"
---
# <a name="stayinsync-property"></a>StayInSync 屬性
表示以階層式[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件是否基礎的子記錄的參考 (也就是*章*) 的父資料列位置變更時的變更。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**布林**值。 預設值為 **True**。 如果 **，則為 True**，將更新的章節，如果父代**資料錄集**物件變更資料列位置; 如果**False**，本章將繼續參考前一章中的資料即使父代**資料錄集**物件已變更的資料列位置。  
  
## <a name="remarks"></a>備註  
 此屬性會套用至階層式資料錄集的郵件，例如支援[Microsoft Data Shaping Service 的 OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)，而且必須設定其父系**資料錄集**子系之前**資料錄集**擷取。 這個屬性可簡化瀏覽階層式資料錄集。  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [StayInSync 屬性範例 (VB)](../../../ado/reference/ado-api/stayinsync-property-example-vb.md)   
 [Microsoft 資料成形 OLE DB （ADO 服務提供者） 的服務](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)

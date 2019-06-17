---
title: 調整形狀名稱動態屬性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Reshape Name property [ADO]
ms.assetid: 690229d1-46cc-42e6-a57d-4438251fe248
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f9b8898a3cc75cf47ae783a1dd2a120c8954ab8f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66711661"
---
# <a name="reshape-name-property-dynamic-ado"></a>Reshape Name 動態屬性 (ADO)
指定的名稱[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件。  
  
## <a name="return-values"></a>傳回值  
 傳回**字串**值，這是名稱**資料錄集**。  
  
## <a name="remarks"></a>備註  
 名稱保存期間內的連接，或直到**資料錄集**已關閉。  
  
 **調整形狀名稱**屬性主要是用於重新成形功能[Microsoft Data Shaping Service 的 OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)服務提供者。 名稱必須是唯一參與重新塑造。  
  
 這個屬性是唯讀的但可以設定間接何時**資料錄集**建立。 例如，如果子句 Shape 命令會建立**資料錄集**並為其使用提供的別名**AS**關鍵字，別名指派給**調整形狀名稱**屬性。 如果已宣告沒有別名，**調整形狀名稱**屬性會被指派資料成形服務所產生的唯一名稱。 別名名稱是否與現有名稱相同**Recordset**，不**資料錄集**可重繪，直到其中一個被釋放為止。 設定中唯一的名稱也可以變更預設行為[調整形狀名稱](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md)上的 ADO 連接屬性 **，則為 True**。 設定這個屬性可讓資料成形服務的權限變更指派的使用者名稱，如有必要，以確保唯一性。 如需重整的詳細資訊，請參閱[Microsoft Data Shaping Service 的 OLE DB （ADO 服務提供者）](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)。  
  
 使用**調整形狀名稱**屬性，當您想要參考**資料錄集**在圖形的命令中，或因為由 Data Shaping Service 產生的它不知道的名稱。 在此情況下，您無法產生圖形命令，藉由串連命令所傳回的字串周圍**調整形狀名稱**屬性。  
  
 **調整形狀名稱**動態屬性附加至**Recordset**物件的[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合時[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性設定為**adUseClient**。  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft 資料成形 OLE DB （ADO 服務提供者） 的服務](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)   
 [一般 shape 命令](../../../ado/guide/data/shape-commands-in-general.md)   
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)

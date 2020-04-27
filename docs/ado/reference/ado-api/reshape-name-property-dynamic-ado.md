---
title: 重新調整名稱屬性-動態（ADO） |Microsoft Docs
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
ms.openlocfilehash: ec72b2b1908f967caee4610e27315acaab787ac9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "67917176"
---
# <a name="reshape-name-property-dynamic-ado"></a>Reshape Name 動態屬性 (ADO)
指定[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件的名稱。  
  
## <a name="return-values"></a>傳回值  
 傳回**字串**值，這是**記錄集**的名稱。  
  
## <a name="remarks"></a>備註  
 名稱會保存在連接的持續時間內，或直到**記錄集**關閉為止。  
  
 [重設**名稱**] 屬性主要是用於 OLE DB 服務提供者的[Microsoft 資料成形服務](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)的重新成形功能。 名稱必須是唯一的，才能參與重新塑造。  
  
 這個屬性是唯讀的，但是可以在建立**記錄集**時間接設定。 例如，如果 Shape 命令的子句建立**記錄集**，並使用**AS**關鍵字提供別名名稱，則別名會指派給 [重設**名稱**] 屬性。 如果未宣告別名，則會將資料成形服務所產生的唯一名稱指派給 [重設**名稱**] 屬性。 如果別名名稱與現有**記錄集**的名稱相同，則不會對**記錄集**進行整形，直到其中一項已釋放為止。 在 ADO 連接的 [重新[調整名稱](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md)] 屬性中設定唯一名稱，即可變更預設行為**True**。 設定此屬性可讓資料成形服務許可權變更使用者指派的名稱（如有必要），以確保唯一性。 如需重新塑造的詳細資訊，請參閱[適用于 OLE DB 的 Microsoft 資料成形服務（ADO 服務提供者）](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)。  
  
 當您想要參考圖形命令中的**記錄集**時，或當您不知道名稱，因為它是由資料成形服務所產生時，請使用 [重新**調整名稱**] 屬性。 在此情況下，您可以將命令與 [調整大小 **] 屬性所**傳回的字串串連在一起，以產生圖形命令。  
  
 當[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性設定為**adUseClient**時，重新**整形名稱**是附加至**記錄集**物件之[Properties](../../../ado/reference/ado-api/properties-collection-ado.md)集合的動態屬性。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [適用于 OLE DB 的 Microsoft 資料成形服務（ADO 服務提供者）](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)   
 [一般的圖形命令](../../../ado/guide/data/shape-commands-in-general.md)   
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)

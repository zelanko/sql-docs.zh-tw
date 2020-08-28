---
description: Reshape Name 動態屬性 (ADO)
title: 重新調整 Name 屬性-Dynamic (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Reshape Name property [ADO]
ms.assetid: 690229d1-46cc-42e6-a57d-4438251fe248
author: rothja
ms.author: jroth
ms.openlocfilehash: dbffa574fd9746788c38b6c03d9690a91ff89730
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989539"
---
# <a name="reshape-name-property-dynamic-ado"></a>Reshape Name 動態屬性 (ADO)
指定 [記錄集](./recordset-object-ado.md) 物件的名稱。  
  
## <a name="return-values"></a>傳回值  
 傳回 **字串** 值，這是 **記錄集**的名稱。  
  
## <a name="remarks"></a>備註  
 名稱會保存在連接期間，或直到 **記錄集** 關閉為止。  
  
 重設 **形狀名稱** 屬性主要是用於 OLE DB 服務提供者的 [Microsoft 資料成形服務](../../guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) 的重成形功能。 名稱必須是唯一的，才能參與重新成形。  
  
 這個屬性是唯讀的，但可以在建立 **記錄集** 時間接設定。 例如，如果 Shape 命令的子句建立 **記錄集** ，並使用 **AS** 關鍵字為它命名別名，則會將別名指派給重設程式 **名稱** 屬性。 如果未宣告任何別名，就會將資料成形服務所產生的唯一名稱指派給重設程式 **名稱** 屬性。 如果別名名稱與現有 **記錄集**的名稱相同，則在其中一個記錄集發行之前，都不會改變 **記錄集** 。 您可以在 ADO 連接的 [重設程式 [名稱]() ] 屬性中，將唯一名稱設定為 **True**，藉以變更預設行為。 如果有必要，設定此屬性會提供資料成形服務許可權來變更使用者指派的名稱，以確保唯一性。 如需重構的詳細資訊，請參閱 [OLE DB (ADO 服務提供者) 的 Microsoft 資料成形服務 ](../../guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)。  
  
 當您想要參考圖形命令中的**記錄集**時，或當您不知道名稱，因為它是由資料成形服務所產生時，請使用 [重設**名稱**] 屬性。 在這種情況下，您可以在調整大小的 **名稱** 屬性所傳回的字串周圍串連命令，以產生 SHAPE 命令。  
  
 當[CursorLocation](./cursorlocation-property-ado.md)屬性設定為**adUseClient**時，重設**名稱**是在**記錄集**物件的[Properties](./properties-collection-ado.md)集合附加的動態屬性。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [適用于 OLE DB (ADO 服務提供者的 Microsoft 資料成形服務) ](../../guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)   
 [一般圖形命令](../../guide/data/shape-commands-in-general.md)   
 [Recordset 物件 (ADO)](./recordset-object-ado.md)
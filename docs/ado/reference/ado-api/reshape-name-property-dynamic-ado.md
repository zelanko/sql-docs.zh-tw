---
title: "重繪名稱屬性動態 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords: Reshape Name property [ADO]
ms.assetid: 690229d1-46cc-42e6-a57d-4438251fe248
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8e18334a3e438ed484f24382e4a84f0a278747ea
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="reshape-name-property-dynamic-ado"></a>重繪名稱屬性動態 (ADO)
指定的名稱[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件。  
  
## <a name="return-values"></a>傳回值  
 傳回**字串**也就是值的名稱**資料錄集**。  
  
## <a name="remarks"></a>備註  
 名稱保存期間內的連接，或直到**資料錄集**已關閉。  
  
 **重繪名稱**屬性主要是供與重新塑造功能搭配使用[Microsoft Data Shaping Service 的 OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)服務提供者。 名稱必須是唯一參與重新成形。  
  
 這個屬性是唯讀的但您可以將間接當**資料錄集**建立。 例如，如果子句 Shape 命令會建立**資料錄集**，並讓它的別名名稱使用**AS**關鍵字，別名指派給**重繪名稱**屬性。 如果宣告沒有別名，**重繪名稱**屬性會被指派資料成形服務所產生的唯一名稱。 如果別名名稱與現有名稱相同**資料錄集**，都不**資料錄集**可重繪，直到其中一個釋放為止。 設定中唯一的名稱也可以變更預設行為[重繪名稱](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md)ADO 連接上的屬性**True**。 設定這個屬性提供用來形成服務權限，若要變更指派的使用者名稱，如有必要，來確保唯一性的資料。 如需才可遏制的詳細資訊，請參閱[Microsoft Data Shaping Service 的 OLE DB （ADO 服務提供者）](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)。  
  
 使用**重繪名稱**屬性，當您想要參考**資料錄集**在圖形命令中，或因為它由 Data Shaping Service 產生不知道名稱。 在此情況下，您可以藉由串連所傳回的字串前後命令產生 SHAPE 命令**重繪名稱**屬性。  
  
 **重繪名稱**動態屬性附加至**資料錄集**物件的[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合時[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性設定為**adUseClient**。  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>請參閱  
 [Microsoft 資料成形 OLE DB （ADO 服務提供者） 的服務](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)   
 [在一般的圖形命令](../../../ado/guide/data/shape-commands-in-general.md)   
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)

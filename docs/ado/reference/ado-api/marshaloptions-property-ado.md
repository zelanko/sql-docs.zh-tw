---
description: MarshalOptions 屬性 (ADO)
title: " (ADO) 的 MarshalOptions 屬性 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::MarshalOptions
helpviewer_keywords:
- MarshalOptions property [ADO]
ms.assetid: 390c8abf-133e-40da-8b99-8f748a983e4f
author: rothja
ms.author: jroth
ms.openlocfilehash: a3eb985c5940659f6d70c331dd860f0588398fb8
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88774497"
---
# <a name="marshaloptions-property-ado"></a>MarshalOptions 屬性 (ADO)
指出要將記錄 [集](./recordset-object-ado.md) 重新封送處理回伺服器的記錄。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回 [MarshalOptionsEnum](./marshaloptionsenum.md) 值。 預設值為 **adMarshalAll**。  
  
## <a name="remarks"></a>備註  
 使用用戶端 [記錄集](./recordset-object-ado.md)時，在用戶端上修改的記錄會透過稱為封送處理的技術，寫回仲介層或 Web 服務器，這是線上程或進程界限之間封裝和傳送介面方法參數的程式。 當修改的遠端資料被封送處理，以更新回仲介層或網頁伺服器時，設定 **MarshalOptions** 屬性可以改善效能。  
  
> [!NOTE]
>  **遠端資料服務使用量** 這個屬性只會在用戶端 **記錄集**上使用。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (VB) 的 MarshalOptions 屬性範例 ](./marshaloptions-property-example-vb.md)   
 [MarshalOptions 屬性範例 (VC++)](./marshaloptions-property-example-vc.md)
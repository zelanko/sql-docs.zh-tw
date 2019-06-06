---
title: DefaultDatabase 屬性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::DefaultDatabase
helpviewer_keywords:
- DefaultDatabase property
ms.assetid: 41e8a8dd-e69c-4a09-8736-93502e01961c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 2eb89353c29ae58194f89b48502f0a9cc5522b58
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66695448"
---
# <a name="defaultdatabase-property"></a>DefaultDatabase 屬性
表示的預設資料庫[連線](../../../ado/reference/ado-api/connection-object-ado.md)物件。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**字串**評估為可用資料庫的名稱，從提供者的值。  
  
## <a name="remarks"></a>備註  
 使用**DefaultDatabase**屬性來設定或傳回的預設資料庫的名稱在特定**連線**物件。  
  
 如果沒有預設的資料庫，SQL 字串可能使用不合格的語法來存取該資料庫中的物件。 若要存取物件中所指定以外的資料庫中**DefaultDatabase**屬性，您必須以限定物件名稱所需的資料庫名稱。 連接時，提供者將預設資料庫會將資訊寫入**DefaultDatabase**屬性。 某些提供者允許每個連接的只有一個資料庫，請在此情況下，您無法變更**DefaultDatabase**屬性。  
  
 某些資料來源和提供者可能不支援這項功能，並可能會傳回錯誤或空字串。  
  
> [!NOTE]
>  **遠端資料服務使用量**這個屬性並不適用於用戶端**連線**物件。  
  
## <a name="applies-to"></a>適用於  
 [Connection 物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Provider 和 DefaultDatabase 屬性範例 (VB)](../../../ado/reference/ado-api/provider-and-defaultdatabase-properties-example-vb.md)   
 [Provider 和 DefaultDatabase 屬性範例 (VC++)](../../../ado/reference/ado-api/provider-and-defaultdatabase-properties-example-vc.md)   

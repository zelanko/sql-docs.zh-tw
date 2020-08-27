---
description: DefaultDatabase 屬性
title: DefaultDatabase 屬性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 86a8b283880f0765100c5a36eb63954f232c565a
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88974189"
---
# <a name="defaultdatabase-property"></a>DefaultDatabase 屬性
表示 [連接](../../../ado/reference/ado-api/connection-object-ado.md) 物件的預設資料庫。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回 **字串** 值，此值會評估為提供者提供的資料庫名稱。  
  
## <a name="remarks"></a>備註  
 您可以使用 **DefaultDatabase** 屬性，在特定的 **連接** 物件上設定或傳回預設資料庫的名稱。  
  
 如果有預設資料庫，SQL 字串可能會使用不合格的語法來存取該資料庫中的物件。 若要存取資料庫中的物件，而非 **DefaultDatabase** 屬性中指定的物件，您必須使用所需的資料庫名稱來限定物件名稱。 連接時，提供者會將預設資料庫資訊寫入至 **DefaultDatabase** 屬性。 有些提供者每個連接只允許一個資料庫，在這種情況下，您無法變更 **DefaultDatabase** 屬性。  
  
 某些資料來源和提供者可能不支援這項功能，而且可能會傳回錯誤或空字串。  
  
> [!NOTE]
>  **遠端資料服務使用量** 用戶端 **連接** 物件上無法使用這個屬性。  
  
## <a name="applies-to"></a>套用至  
 [Connection 物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Provider 和 DefaultDatabase 屬性範例 (VB) ](../../../ado/reference/ado-api/provider-and-defaultdatabase-properties-example-vb.md)   
 [Provider 和 DefaultDatabase 屬性範例 (VC++)](../../../ado/reference/ado-api/provider-and-defaultdatabase-properties-example-vc.md)   

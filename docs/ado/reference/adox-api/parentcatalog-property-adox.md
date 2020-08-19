---
description: ParentCatalog 屬性 (ADOX)
title: ParentCatalog 屬性 (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _User::get_ParentCatalog
- _Column::ParentCatalog
- _Table::put_ParentCatalog
- _Group::put_ParentCatalog
- _Column::get_ParentCatalog
- _Table::PutParentCatalog
- _Group::putref_ParentCatalog
- _Group::ParentCatalog
- _Column::PutParentCatalog
- _Column::put_ParentCatalog
- _Group::get_ParentCatalog
- _User::put_ParentCatalog
- _User::putref_ParentCatalog
- _Table::get_ParentCatalog
- _Group::PutParentCatalog
- _Table::ParentCatalog
- _Column::GetParentCatalog
- _Table::PutRefParentCatalog
- _User::GetParentCatalog
- _Table::GetParentCatalog
- _Table::putref_ParentCatalog
- _User::PutParentCatalog
- _User::ParentCatalog
- _User::PutRefParentCatalog
- _Group::GetParentCatalog
- _Group::PutRefParentCatalog
helpviewer_keywords:
- ParentCatalog property [ADOX]
ms.assetid: a0bb2ed8-d4cb-4f92-8de7-769bbe0e6273
author: rothja
ms.author: jroth
ms.openlocfilehash: 93d15cdac3d8f7a47c74a783d176d806271f68a3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88439720"
---
# <a name="parentcatalog-property-adox"></a>ParentCatalog 屬性 (ADOX)
指定資料表、使用者或資料行物件的父類別目錄，以提供對提供者特定屬性的存取權。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定並傳回 [目錄](../../../ado/reference/adox-api/catalog-object-adox.md) 物件。 將 **ParentCatalog** 設定為開啟 **目錄** ，可在將資料表或資料行附加至 **目錄** 集合之前，允許存取提供者特有的屬性。  
  
## <a name="remarks"></a>備註  
 有些資料提供者只允許在建立時寫入提供者專屬的屬性值，也就是將資料表或資料行附加至其 **目錄** 集合時。 若要在將這些物件附加至**目錄**之前先存取這些屬性，請先在**ParentCatalog**屬性中指定**目錄**。  
  
 當資料表或資料行附加至與**ParentCatalog**不同的**目錄**時，就會發生錯誤。  
  
## <a name="applies-to"></a>套用至  

:::row:::
    :::column:::
        [Column 物件 (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)  
    :::column-end:::
    :::column:::
        [Table 物件 (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)  
    :::column-end:::
    :::column:::
        [User 物件 (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另請參閱  
 [ParentCatalog 屬性範例 (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)

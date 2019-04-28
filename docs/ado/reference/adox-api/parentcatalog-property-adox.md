---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 10d6715a19212c87ece9c890ee99516571713d4f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62710340"
---
# <a name="parentcatalog-property-adox"></a>ParentCatalog 屬性 (ADOX)
指定的父目錄的資料表、 使用者或資料行的物件，來提供提供者特定屬性的存取權。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定，並傳回[目錄](../../../ado/reference/adox-api/catalog-object-adox.md)物件。 設定**ParentCatalog**來開啟**類別目錄**允許之前附加的資料表或資料行的提供者特定屬性的存取權**目錄**集合。  
  
## <a name="remarks"></a>備註  
 某些資料提供者允許提供者特有的屬性值只能在建立時寫入： 也就是當資料表或資料行附加至其**目錄**集合。 若要存取這些屬性附加至這些物件之前**類別目錄**，指定**類別目錄**中**ParentCatalog**屬性第一次。  
  
 當資料表或資料行附加至不同而發生錯誤**Catalog**比**ParentCatalog**。  
  
## <a name="applies-to"></a>適用於  
  
|||  
|-|-|  
|[Column 物件 (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)|[Table 物件 (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)|  
|[User 物件 (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)||  
  
## <a name="see-also"></a>另請參閱  
 [ParentCatalog 屬性範例 (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)

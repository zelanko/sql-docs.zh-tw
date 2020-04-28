---
title: ParentCatalog 屬性（ADOX） |Microsoft Docs
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
ms.openlocfilehash: 8bc9527109aaa4a3a8063b26a594c9bdb978dcf3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67965580"
---
# <a name="parentcatalog-property-adox"></a>ParentCatalog 屬性 (ADOX)
指定資料表、使用者或資料行物件的父目錄，以提供提供者特定屬性的存取權。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定並傳回[目錄](../../../ado/reference/adox-api/catalog-object-adox.md)物件。 將**ParentCatalog**設定為開啟的**目錄**，可讓您在將資料表或資料行附加至**目錄**集合之前，先存取提供者特有的屬性。  
  
## <a name="remarks"></a>備註  
 有些資料提供者只允許在建立時寫入提供者特定的屬性值，也就是當資料表或資料行附加至其**類別目錄**集合時。 若要先存取這些屬性，再將這些物件附加至**目錄**，請先在**ParentCatalog**屬性中指定**目錄**。  
  
 當資料表或資料行附加至與**ParentCatalog**不同的**目錄**時，就會發生錯誤。  
  
## <a name="applies-to"></a>套用至  
  
|||  
|-|-|  
|[Column 物件 (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)|[Table 物件 (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)|  
|[User 物件 (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)||  
  
## <a name="see-also"></a>另請參閱  
 [ParentCatalog 屬性範例 (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)

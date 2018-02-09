---
title: "Append 方法 （ADOX 資料行） |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Columns::raw_Append
- Columns::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 7a46d23c-efef-4ec7-815d-cd3ac86787dd
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3e67dc9f6240e94dea2e4494906453ba8e4cfad1
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="append-method-adox-columns"></a>Append 方法 （ADOX 資料行）
將新[資料行](../../../ado/reference/adox-api/column-object-adox.md)物件[資料行](../../../ado/reference/adox-api/columns-collection-adox.md)集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
Columns.Append Column [,Type] [,DefinedSize]  
```  
  
#### <a name="parameters"></a>參數  
 *[資料行]*  
 **資料行**来附加物件或建立並附加至資料行的名稱。  
  
 *型別*  
 選擇性。 A**長**值，指定資料行的資料類型。 *類型*參數會對應至[類型](../../../ado/reference/adox-api/type-property-column-adox.md)屬性**資料行**物件。  
  
 *DefinedSize*  
 選擇性。 A**長**值，指定資料行的大小。 *DefinedSize*參數會對應至[DefinedSize](../../../ado/reference/adox-api/definedsize-property-adox.md)屬性**資料行**物件。  
  
> [!NOTE]
>  當附加時，會發生錯誤**資料行**至**資料行**集合[索引](../../../ado/reference/adox-api/index-object-adox.md)如果**資料行**不存在於[資料表](../../../ado/reference/adox-api/table-object-adox.md)已經附加至[資料表](../../../ado/reference/adox-api/tables-collection-adox.md)集合。  
  
## <a name="applies-to"></a>適用於  
 [Columns 集合 (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)  
  
## <a name="see-also"></a>另請參閱  
 [資料行和資料表附加名稱屬性範例 (VB) 方法](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [索引鍵附加方法、 金鑰類型、 RelatedColumn、 RelatedTable 和 UpdateRule 屬性範例 (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [ParentCatalog 屬性範例 (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [Append 方法 （ADOX 群組）](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append 方法 （ADOX 索引）](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append 方法 （ADOX 索引鍵）](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append 方法 （ADOX 程序）](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append 方法 （ADOX 資料表）](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append 方法 （ADOX 使用者）](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append 方法 (ADOX Views)](../../../ado/reference/adox-api/append-method-adox-views.md)

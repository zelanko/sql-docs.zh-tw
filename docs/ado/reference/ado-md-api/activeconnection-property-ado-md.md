---
title: ActiveConnection 屬性 (ADO MD) |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ActiveConnection
- Cellset::ActiveConnection
- Catalog::ActiveConnection
helpviewer_keywords:
- ActiveConnection property [ADO MD]
ms.assetid: 2509b32c-a995-4364-9152-d8c83129bdd8
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6a26da86e21799aa18f3c3a4b190eb1636401e5d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="activeconnection-property-ado-md"></a>ActiveConnection 屬性 (ADO MD)
表示要哪些 ADO[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件目前的資料格集或目前所屬的目錄。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**Variant** ，其中包含定義連接字串或**連接**物件。 預設值是空的。  
  
## <a name="remarks"></a>備註  
 您可以將此屬性設定為有效的 ADO**連接**物件或為有效的連接字串。 當這個屬性設定為連接字串時，建立新的提供者**連接**物件使用這個定義，並開啟連接。  
  
 如果您使用*ActiveConnection*引數的[開啟](../../../ado/reference/ado-md-api/open-method-ado-md.md)方法來開啟[資料格集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)物件**ActiveConnection**屬性繼承的引數的值。  
  
 設定**ActiveConnection**屬性[目錄](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)物件**Nothing**釋放相關聯的資料，包括中的資料[CubeDefs](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)集合，以及任何相關[維度](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)，[階層](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)，[層級](../../../ado/reference/ado-md-api/level-object-ado-md.md)，和[成員](../../../ado/reference/ado-md-api/member-object-ado-md.md)物件。 關閉**連接**物件，用來開啟**目錄**已設定相同的效果**ActiveConnection**屬性**Nothing**.  
  
 所參考之連接的預設資料庫進行變更**ActiveConnection**屬性**目錄**物件會導致無效的內容**目錄**。  
  
 如果您嘗試變更，會發生錯誤**ActiveConnection**屬性為開啟**資料格集**物件。  
  
> [!NOTE]
>  在 Visual Basic，請務必使用**設定**關鍵字設定時**ActiveConnection**屬性**連接**物件。 如果您省略**設定**關鍵字，您會實際設定**ActiveConnection**屬性等於**連接**物件的預設屬性， **ConnectionString**。 程式碼能夠運作。不過，您將建立資料來源，這可能會有負面的效能含意的其他連接。  
  
 使用時的 MSOLAP 資料提供者，資料來源連接字串中設定為伺服器名稱和初始目錄設類別目錄的名稱，從資料來源。 若要連接到伺服器中斷連接時的 cube 檔案，將位置設定的完整路徑。CUB 檔案。 在任一情況下，設定提供者的提供者名稱。 例如，下列字串會使用 MSOLAP 提供者連接到名為的伺服器上名為 Bobs 視訊存放區目錄**Servername**:  
  
```  
"Data Source=Servername;Initial Catalog=Bobs Video Store;Provider=msolap"  
```  
  
 下列字串會連接到本機 cube 檔案的位置 C:\MSDASDK\samples\oledb\olap\data\bobsvid.cub:  
  
```  
"Location=C:\MSDASDK\samples\oledb\olap\data\bobsvid.cub;Provider=msolap"  
```  
  
## <a name="applies-to"></a>適用於  
  
|||  
|-|-|  
|[Catalog 物件 (ADO MD)](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)|[Cellset 物件 (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)|  
  
## <a name="see-also"></a>另請參閱  
 [資料格集範例 (VB)](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [連接物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Open 方法 (ADO MD)](../../../ado/reference/ado-md-api/open-method-ado-md.md)

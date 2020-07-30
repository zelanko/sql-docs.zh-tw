---
title: ActiveConnection 屬性（ADO MD） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ActiveConnection
- Cellset::ActiveConnection
- Catalog::ActiveConnection
helpviewer_keywords:
- ActiveConnection property [ADO MD]
ms.assetid: 2509b32c-a995-4364-9152-d8c83129bdd8
author: rothja
ms.author: jroth
ms.openlocfilehash: 5e504b442116f0a137d40a0932b00e51753deae5
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87243149"
---
# <a name="activeconnection-property-ado-md"></a>ActiveConnection 屬性 (ADO MD)
指出目前的儲存格或目錄目前所屬的 ADO[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回包含定義連接或**連接**物件之字串的**Variant** 。 預設值是空的。  
  
## <a name="remarks"></a>備註  
 您可以將此屬性設定為有效的 ADO**連接**物件或有效的連接字串。 當這個屬性設定為連接字串時，提供者會使用此定義來建立新的**連接**物件，並開啟連接。  
  
 如果您使用[open](../../../ado/reference/ado-md-api/open-method-ado-md.md)方法的*ActiveConnection*引數來開啟「[集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)」物件，則**ActiveConnection**屬性會繼承引數的值。  
  
 將[目錄](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)物件的**ActiveConnection**屬性**設定為不**會釋出相關聯的資料，包括[CubeDefs](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)集合中的[資料，以及](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)任何相關的[維度](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)、階層、[層級](../../../ado/reference/ado-md-api/level-object-ado-md.md)和[成員](../../../ado/reference/ado-md-api/member-object-ado-md.md)物件。 關閉用來開啟**目錄**的**連接**物件，其效果與將**ActiveConnection**屬性設定為 [**無**] 相同。  
  
 變更**目錄**物件的**ActiveConnection**屬性所參考之連接的預設資料庫，會使**目錄**的內容失效。  
  
 如果您嘗試變更開啟的**儲存格集**物件的**ActiveConnection**屬性，就會發生錯誤。  
  
> [!NOTE]
>  在 Visual Basic 中，請記得在將**ActiveConnection**屬性設定為**連接**物件時，使用**Set**關鍵字。 如果您省略**Set**關鍵字，實際上您會將**ActiveConnection**屬性設定為等於**Connection**物件的 default 屬性**ConnectionString**。 程式碼會正常執行;不過，您將建立與資料來源的額外連接，這可能會對效能造成負面影響。  
  
 使用 MSOLAP 資料提供者時，請將連接字串中的資料來源設定為伺服器名稱，並將初始目錄設定為數據源中的目錄名稱。 若要連接到與伺服器中斷連接的 cube 檔案，請將 [位置] 設定為的完整路徑。.CUB 檔案。 不論是哪一種情況，請將提供者設定為提供者名稱。 例如，下列字串會使用 MSOLAP 提供者，連接到名為**Servername**之伺服器上名為 bobs-machine 的目錄：  
  
```  
"Data Source=Servername;Initial Catalog=Bobs Video Store;Provider=msolap"  
```  
  
 下列字串會連接到位置 C:\MSDASDK\samples\oledb\olap\data\bobsvid.cub 的本機 cube 檔案：  
  
```  
"Location=C:\MSDASDK\samples\oledb\olap\data\bobsvid.cub;Provider=msolap"  
```  
  
## <a name="applies-to"></a>套用至  

:::row:::
    :::column:::
        [Catalog 物件 (ADO MD)](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)  
    :::column-end:::
    :::column:::
        [Cellset 物件 (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另請參閱  
 [格集範例（VB）](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [Connection 物件（ADO）](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Open 方法 (ADO MD)](../../../ado/reference/ado-md-api/open-method-ado-md.md)

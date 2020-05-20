---
title: Create 方法（ADOX） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Catalog::raw_Create
- _Catalog::Create
helpviewer_keywords:
- Create method [ADOX]
ms.assetid: 64f5c21c-b581-42d8-bdc7-c4f1bebaf105
author: rothja
ms.author: jroth
ms.openlocfilehash: 15ea5cf8b565a943f4905a890cb08ba0afed202f
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759264"
---
# <a name="create-method-adox"></a>Create 方法 (ADOX)
建立新的目錄。  
  
## <a name="syntax"></a>語法  
  
```  
  
Catalog.Create ConnectString  
```  
  
#### <a name="parameters"></a>參數  
 *ConnectString*  
 用來連接到資料來源的**字串**值。  
  
## <a name="remarks"></a>備註  
 **Create**方法會建立並開啟新的 ADO[連接](../../../ado/reference/ado-api/connection-object-ado.md)，以連線至*ConnectString*中指定的資料來源。 如果成功，就會將新的**連接**物件指派給[ActiveConnection](../../../ado/reference/adox-api/activeconnection-property-adox.md)屬性。  
  
 如果提供者不支援建立新的目錄，就會發生錯誤。  
  
## <a name="applies-to"></a>套用至  
 [Catalog 物件 (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)  
  
## <a name="see-also"></a>另請參閱  
 [Create 方法範例（VB）](../../../ado/reference/adox-api/create-method-example-vb.md)   
 [ActiveConnection 屬性 (ADOX)](../../../ado/reference/adox-api/activeconnection-property-adox.md)

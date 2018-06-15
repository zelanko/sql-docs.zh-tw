---
title: 'Isscommandwithparameters:: (OLE DB) |Microsoft 文件'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISSCommandWithParameters::SetParameterProperties (OLE DB)
apitype: COM
helpviewer_keywords:
- SetParameterProperties method
ms.assetid: 4cd0281a-a2a0-43df-8e46-eb478b64cb4b
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: dbd38ed336375cef79119f2fafb565bceeeb85bd
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32949163"
---
# <a name="isscommandwithparameterssetparameterproperties-ole-db"></a>ISSCommandWithParameters::SetParameterProperties (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  依照序數根據每個參數來設定參數的屬性，或指定 SSPARAMPROPS 結構的陣列來設定大量參數屬性。  
  
## <a name="syntax"></a>語法  
  
```  
  
HRESULT SetParameterProperties(  
      DB_UPARAMS cParams,   
      SSPARAMPROPS rgParamProperties[]);  
```  
  
## <a name="arguments"></a>引數  
 *cParams*[in]  
 中的數字的 SSPARAMPROPS 結構*rgParamProperties*陣列。 如果這個數字為零， **isscommandwithparameters::** 將會刪除所有可能的任何參數，在命令中指定的屬性。  
  
 *rgParamProperties*[in]  
 要設定的 SSPARAMPROPS 結構的陣列。  
  
## <a name="return-code-values"></a>傳回碼值  
 **Isscommandwithparameters::** 方法會傳回相同的錯誤碼與核心 OLE DB **icommandproperties:: Setproperties**方法。  
  
## <a name="remarks"></a>備註  
 使用這個方法來設定參數屬性上每個參數來允許依序數，或使用單一**isscommandwithparameters::** 從屬性陣列建立 SSPARAMPROPS 之後呼叫。  
  
 **SetParameterInfo**必須呼叫方法，然後再呼叫**isscommandwithparameters::** 方法。 呼叫 `SetParameterProperties(0, NULL)` 會清除所有指定的參數屬性，呼叫 `SetParameterInfo(0,NULL,NULL)` 則會清除所有的參數資訊，包括任何可能與參數相關聯的屬性。  
  
 呼叫**isscommandwithparameters::** 指定的參數而不是型別內容 DBTYPE_XML 或 DBTYPE_UDT 會傳回 DB_E_ERRORSOCCURRED 或 DB_S_ERRORSOCCURRED，並*dwStatus*所有 DBPROPs SSPARAMPROPS 中包含具有 DBPROPSTATUS_NOTSET 的該參數的欄位。 系統會周遊 SSPARAMPROPS 中包含的每個 DBPROPSET 的 DBPROP 陣列，以偵測 DB_E_ERRORSOCCURRED 或 DB_S_ERRORSOCCURRED 所參考的是哪一個參數。  
  
 如果**isscommandwithparameters::** 呼叫以指定的參數尚未尚未設定其參數資訊，與屬性**SetParameterInfo**，提供者會傳回 E_非預期的使用下列的錯誤訊息：  
  
 必須先針對指定的參數呼叫 SetParameterInfo 方法，然後才能呼叫 SetParameterProperties 方法。 而在設定參數屬性之前，也必須先設定參數資訊。  
  
 如果呼叫**isscommandwithparameters::** 包含的參數資訊，其中已設定，某些參數，以及某些參數，其中參數資訊尚未設定中的 dwStatus 屬性SSPARAMPROPS 屬性集的 DBPROPSET 會以 DBSTATUS_NOTSET 傳回。  
  
 SSPARAMPROPS 結構定義如下：  
  
 `struct SSPARAMPROPS {`  
  
 `DBORDINAL iOrdinal;`  
  
 `ULONG cPropertySets;`  
  
 `DBPROPSET *rgPropertySets;`  
  
 `};`  
  
 開始 database engine 中的增強功能[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]允許 isscommandwithparameters:: 若要取得更精確的預期結果的描述。 這些更精確的結果可能與在舊版的 isscommandwithparameters:: 傳回的值不同[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如需詳細資訊，請參閱[中繼資料探索](../../relational-databases/native-client/features/metadata-discovery.md)。  
  
|成員|Description|  
|------------|-----------------|  
|*iOrdinal*|所傳遞參數的序數。|  
|*cPropertySets*|的 DBPROPSET 結構數目中*rgPropertySets*。|  
|*rgPropertySets*|藉其傳回 DBPROPSET 結構陣列的記憶體指標。|  
  
## <a name="see-also"></a>另請參閱  
 [ISSCommandWithParameters & #40; OLE DB & #41;](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  

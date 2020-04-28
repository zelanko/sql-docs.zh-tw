---
title: ISSCommandWithParameters::GetParameterProperties (OLE DB)
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- ISSCommandWithParameters::GetParameterProperties (OLE DB)
apitype: COM
helpviewer_keywords:
- GetParameterProperties method
ms.assetid: 7f4cc5ea-d028-4fe5-9192-bd153ab3c26c
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 26c95c64f0f2922ef11946841b160879f001e358
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81290068"
---
# <a name="isscommandwithparametersgetparameterproperties-ole-db"></a>ISSCommandWithParameters::GetParameterProperties (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  傳回 SSPARAMPROPS 屬性集結構的陣列，而且每個 UDT 或 XML 參數使用一個 SSPARAMPROPS 屬性集。  
  
## <a name="syntax"></a>語法  
  
```cpp
HRESULT GetParameterProperties(  
      DB_UPARAMS *pcParams,  
      SSPARAMPROPS **prgParamProperties);  
```  
  
## <a name="arguments"></a>引數  
 *pcParams*[out][in]  
 記憶體的指標，其中包含在 *prgParamProperties* 中傳回的 SSPARAMPROPS 結構數目。  
  
 *prgParamProperties*[out]  
 藉其傳回 SSPARAMPROPS 結構陣列的記憶體指標。 提供者會為結構配置記憶體，並將位址傳回此記憶體;取用者不再需要結構時，會使用**IMalloc：： Free**釋放此記憶體。 在呼叫**IMalloc：： Free** for *prgParamProperties*之前，取用者也必須針對每個 DBPROP 結構的*vValue*屬性呼叫**VariantClear** ，以便在 variant 包含參考型別（例如 BSTR）的情況下，避免發生記憶體流失的情況。如果*時 pcparams*在輸出上為零，或發生 DB_E_ERRORSOCCURRED 以外的錯誤，則提供者不會配置任何記憶體，並可確保*prgParamProperties*在輸出上為 null 指標。  
  
## <a name="return-code-values"></a>傳回碼值  
 **GetParameterProperties**方法會傳回與 Core OLE DB **ICommandProperties：： GetProperties**方法相同的錯誤碼，不同之處在于無法引發 DB_S_ERRORSOCCURRED 和 DB_E_ERRORSOCCURED。  
  
## <a name="remarks"></a>備註  
 **ISSCommandWithParameters：： GetParameterProperties**的行為一致，與**GetParameterInfo**有關。 如果尚未呼叫[ISSCommandWithParameters：： SetParameterProperties](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md)或**SetParameterInfo** ，或已使用 cParams 等於零的呼叫， **GetParameterInfo**會衍生參數資訊，並傳回這個。 如果至少已針對一個參數呼叫**ISSCommandWithParameters：： SetParameterProperties**或**SetParameterInfo** ， **ISSCommandWithParameters：： GetParameterProperties**只會針對已呼叫**ISSCommandWithParameters：： SetParameterProperties**的參數傳回屬性。 如果在**ISSCommandWithParameters：： GetParameterProperties**或**GetParameterInfo**之後呼叫**ISSCommandWithParameters：： SetParameterProperties** ，則對**ISSCommandWithParameters：： GetParameterProperties**的後續呼叫會針對已呼叫**ISSCommandWithParameters：： SetParameterProperties**的參數傳回覆寫的值。  
  
 SSPARAMPROPS 結構定義如下：  

```cpp
struct SSPARAMPROPS {
    DBORDINAL iOrdinal;
    ULONG cPropertySets;
    DBPROPSET *rgPropertySets;
};
```

|member|描述|  
|------------|-----------------|  
|*iOrdinal*|所傳遞參數的序數。|  
|*cPropertySets*|*rgPropertySets* 中的 DBPROPSET 結構數目。|  
|*rgPropertySets*|藉其傳回 DBPROPSET 結構陣列的記憶體指標。|  
|||

## <a name="see-also"></a>另請參閱  
 [ISSCommandWithParameters &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  

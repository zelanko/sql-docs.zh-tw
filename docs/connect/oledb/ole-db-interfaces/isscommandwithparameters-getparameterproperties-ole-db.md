---
title: Getparameterinfo (OLE DB) |Microsoft Docs
description: ISSCommandWithParameters::GetParameterProperties (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: reference
apiname:
- ISSCommandWithParameters::GetParameterProperties (OLE DB)
apitype: COM
helpviewer_keywords:
- GetParameterProperties method
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: a1ff014ff8c3ff412303e6de3506099fca8a4103
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47642236"
---
# <a name="isscommandwithparametersgetparameterproperties-ole-db"></a>ISSCommandWithParameters::GetParameterProperties (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  傳回 SSPARAMPROPS 屬性集結構的陣列，而且每個 UDT 或 XML 參數使用一個 SSPARAMPROPS 屬性集。  
  
## <a name="syntax"></a>語法  
  
```  
  
HRESULT GetParameterProperties(  
      DB_UPARAMS *pcParams,  
      SSPARAMPROPS **prgParamProperties);  
```  
  
## <a name="arguments"></a>引數  
 *pcParams*[out][in]  
 記憶體的指標，其中包含在 *prgParamProperties* 中傳回的 SSPARAMPROPS 結構數目。  
  
 *prgParamProperties*[out]  
 藉其傳回 SSPARAMPROPS 結構陣列的記憶體指標。 提供者會配置用於結構的記憶體，並將地址傳回此記憶體；當它不再需要該結構時，取用者會使用 **IMalloc::Free** 釋放此記憶體。 針對 *prgParamProperties* 呼叫 **IMalloc::Free** 之前，取用者也必須針對每個 DBPROP 結構的 *vValue* 屬性呼叫 **VariantClear**，才能在變數包含參考型別 (例如 BSTR) 時防止記憶體流失。 如果輸出時 *pcParams* 為零，或者發生 DB_E_ERRORSOCCURRED 之外的錯誤，提供者就不會配置任何記憶體，也無法確保輸出時，*prgParamProperties* 為 Null 指標。  
  
## <a name="return-code-values"></a>傳回碼值  
 除了無法引發 DB_S_ERRORSOCCURRED 和 DB_E_ERRORSOCCURED 之外，**GetParameterProperties** 方法會傳回與核心 OLE DB **ICommandProperties::GetProperties** 方法相同的錯誤碼。  
  
## <a name="remarks"></a>Remarks  
 相對於 **GetParameterInfo** 而言，**ISSCommandWithParameters::GetParameterProperties** 方法的行為一致。 如果尚未呼叫 [ISSCommandWithParameters::SetParameterProperties](../../oledb/ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md) 或 **SetParameterInfo**，或者已經在 cParams 等於零的情況下進行呼叫，**GetParameterInfo** 會衍生並傳回參數資訊。 如果至少已經針對一個參數呼叫 **ISSCommandWithParameters::SetParameterProperties** 或 **SetParameterInfo**，**ISSCommandWithParameters::GetParameterProperties** 方法僅會針對已經呼叫 **ISSCommandWithParameters::SetParameterProperties** 的參數傳回屬性。 如果在 **ISSCommandWithParameters::GetParameterProperties** 或 **GetParameterInfo** 之後呼叫 **ISSCommandWithParameters::SetParameterProperties**，**ISSCommandWithParameters::GetParameterProperties** 的後續呼叫會針對已經呼叫 **ISSCommandWithParameters::SetParameterProperties** 方法的參數，傳回覆寫值。  
  
 SSPARAMPROPS 結構定義如下：  
  
 `struct SSPARAMPROPS {`  
  
 `DBORDINAL iOrdinal;`  
  
 `ULONG cPropertySets;`  
  
 `DBPROPSET *rgPropertySets;`  
  
 `};`  
  
|成員|Description|  
|------------|-----------------|  
|*iOrdinal*|所傳遞參數的序數。|  
|*cPropertySets*|*rgPropertySets* 中的 DBPROPSET 結構數目。|  
|*rgPropertySets*|藉其傳回 DBPROPSET 結構陣列的記憶體指標。|  
  
## <a name="see-also"></a>另請參閱  
 [ISSCommandWithParameters &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  

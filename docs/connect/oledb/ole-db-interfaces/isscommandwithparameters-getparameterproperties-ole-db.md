---
title: ISSCommandWithParameters::GetParameterProperties (OLE DB) | Microsoft Docs
description: ISSCommandWithParameters::GetParameterProperties 會傳回 OLE DB Driver for SQL Server 中的屬性集結構陣列，每個 UDT 或 XML 參數各一個。
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- ISSCommandWithParameters::GetParameterProperties (OLE DB)
apitype: COM
helpviewer_keywords:
- GetParameterProperties method
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8631c9c1beed054b57fd368dd567e3568c213b50
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "88862138"
---
# <a name="isscommandwithparametersgetparameterproperties-ole-db"></a>ISSCommandWithParameters::GetParameterProperties (OLE DB)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

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
 藉其傳回 SSPARAMPROPS 結構陣列的記憶體指標。 提供者會配置用於結構的記憶體，並將地址傳回此記憶體；不再需要該結構時，取用者會使用 `IMalloc::Free` 釋放此記憶體。 針對 *prgParamProperties* 呼叫 `IMalloc::Free` 之前，取用者也必須針對每個 DBPROP 結構的 *vValue* 屬性呼叫 `VariantClear`，才能在變數包含參考類型 (例如 BSTR) 時防止記憶體流失。 如果輸出時 *pcParams* 為零，或者發生 DB_E_ERRORSOCCURRED 之外的錯誤，提供者就不會配置任何記憶體，也無法確保輸出時，*prgParamProperties* 為 Null 指標。  
  
## <a name="return-code-values"></a>傳回碼值  
 除了無法引發 DB_S_ERRORSOCCURRED 和 DB_E_ERRORSOCCURED 之外，`GetParameterProperties` 方法會傳回與核心 OLE DB `ICommandProperties::GetProperties` 方法相同的錯誤碼。  
  
## <a name="remarks"></a>備註  
 `ISSCommandWithParameters::GetParameterProperties` 方法的運作方式與 `GetParameterInfo` 一致。 如果尚未呼叫 [ 或 `ISSCommandWithParameters::SetParameterProperties`](../../oledb/ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md)`SetParameterInfo`，或者在 cParams 等於零的情況下進行呼叫，`GetParameterInfo` 將會衍生並傳回參數資訊。 如果至少已對一個參數呼叫了 `ISSCommandWithParameters::SetParameterProperties` 或 `SetParameterInfo`，則 `ISSCommandWithParameters::GetParameterProperties` 方法只會針對已呼叫 `ISSCommandWithParameters::SetParameterProperties` 的參數傳回屬性。 如果在 `ISSCommandWithParameters::GetParameterProperties` 或 `GetParameterInfo` 之後呼叫了 `ISSCommandWithParameters::SetParameterProperties`，後續對 `ISSCommandWithParameters::GetParameterProperties` 的呼叫將會傳回已呼叫 `ISSCommandWithParameters::SetParameterProperties` 方法之參數的覆寫值。  
  
 SSPARAMPROPS 結構定義如下：  
  
 `struct SSPARAMPROPS {`  
  
 `DBORDINAL iOrdinal;`  
  
 `ULONG cPropertySets;`  
  
 `DBPROPSET *rgPropertySets;`  
  
 `};`  
  
|member|描述|  
|------------|-----------------|  
|*iOrdinal*|所傳遞參數的序數。|  
|*cPropertySets*|*rgPropertySets* 中的 DBPROPSET 結構數目。|  
|*rgPropertySets*|藉其傳回 DBPROPSET 結構陣列的記憶體指標。|  
  
## <a name="see-also"></a>另請參閱  
 [ISSCommandWithParameters &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  

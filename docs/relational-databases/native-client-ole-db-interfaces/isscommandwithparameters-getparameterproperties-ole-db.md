---
description: 'ISSCommandWithParameters：： GetParameterProperties in SQL Server Native Client (OLE DB) '
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
ms.openlocfilehash: a0ec5b9666e5b61bfc018825848ca543e42d38c7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88490787"
---
# <a name="isscommandwithparametersgetparameterproperties-in-sql-server-native-client-ole-db"></a>ISSCommandWithParameters：： GetParameterProperties in SQL Server Native Client (OLE DB) 
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

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
 藉其傳回 SSPARAMPROPS 結構陣列的記憶體指標。 提供者會為結構配置記憶體，並將位址傳回給這個記憶體;當取用者不再需要該結構時，會以 **IMalloc：： Free** 釋放此記憶體。 在針對 *>prgparamproperties*呼叫**IMalloc：： Free**之前，取用者也必須針對每個 DBPROP 結構的*vValue*屬性呼叫**VariantClear** ，以避免在變數包含參考型別 (例如 BSTR 的情況下造成記憶體流失。 ) 如果輸出上的*pcParams*為零，或發生 DB_E_ERRORSOCCURRED 以外的錯誤，則提供者不會配置任何記憶體，並確保 *>prgparamproperties*在輸出時為 null 指標。  
  
## <a name="return-code-values"></a>傳回碼值  
 **GetParameterProperties**方法會傳回與 Core OLE DB **ICommandProperties：： GetProperties**方法相同的錯誤碼，但不能引發 DB_S_ERRORSOCCURRED 和 DB_E_ERRORSOCCURED。  
  
## <a name="remarks"></a>備註  
 **ISSCommandWithParameters：： GetParameterProperties** 的行為一致，與 **GetParameterInfo**有關。 如果未呼叫 [ISSCommandWithParameters：： SetParameterProperties](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md) 或 **SetParameterInfo** ，或其 cParams 等於零，則 **GetParameterInfo** 會衍生參數資訊並傳回此值。 如果已針對至少一個參數呼叫 **ISSCommandWithParameters：： SetParameterProperties** 或 **SetParameterInfo** ， **ISSCommandWithParameters：： GetParameterProperties** 只會針對已呼叫 **ISSCommandWithParameters：： SetParameterProperties** 的參數傳回屬性。 如果在**ISSCommandWithParameters：： GetParameterProperties**或**GetParameterInfo**之後呼叫**ISSCommandWithParameters：： SetParameterProperties** ，則對**ISSCommandWithParameters：： GetParameterProperties**的後續呼叫會針對已呼叫**ISSCommandWithParameters：： SetParameterProperties**的參數傳回覆寫的值。  
  
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
  
  

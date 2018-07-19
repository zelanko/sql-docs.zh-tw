---
title: Getparameterinfo (OLE DB) |Microsoft 文件
description: ISSCommandWithParameters::GetParameterProperties (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISSCommandWithParameters::GetParameterProperties (OLE DB)
apitype: COM
helpviewer_keywords:
- GetParameterProperties method
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 9c0f35cd59a670e35db6400f681187c52e4b97ef
ms.sourcegitcommit: 03ba89937daeab08aa410eb03a52f1e0d212b44f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/16/2018
ms.locfileid: "35689991"
---
# <a name="isscommandwithparametersgetparameterproperties-ole-db"></a>ISSCommandWithParameters::GetParameterProperties (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  傳回 SSPARAMPROPS 屬性集結構的陣列，而且每個 UDT 或 XML 參數使用一個 SSPARAMPROPS 屬性集。  
  
## <a name="syntax"></a>語法  
  
```  
  
HRESULT GetParameterProperties(  
      DB_UPARAMS *pcParams,  
      SSPARAMPROPS **prgParamProperties);  
```  
  
## <a name="arguments"></a>引數  
 *pcParams*[in] [out]  
 中包含的 SSPARAMPROPS 結構數目的記憶體指標，傳回*prgParamProperties*。  
  
 *prgParamProperties*[out]  
 藉其傳回 SSPARAMPROPS 結構陣列的記憶體指標。 提供者會為結構配置記憶體，並將位址傳回給這個記憶體取用者釋放此記憶體與**imalloc:: Free**當它不再需要的結構。 然後再呼叫**imalloc:: Free**如*prgParamProperties*，取用者也必須呼叫**Vvalue**如*vValue*屬性若要避免記憶體流失情況下在變數包含參考的每個 DBPROP 結構的類型例如 BSTR。 如果*pcParams*零輸出或發生錯誤 DB_E_ERRORSOCCURRED 之外，提供者不會配置任何記憶體，並確保*prgParamProperties*輸出上的 null 指標。  
  
## <a name="return-code-values"></a>傳回碼值  
 **GetParameterProperties**方法會傳回相同的錯誤碼與核心 OLE DB **icommandproperties:: Getproperties**無法方法，除了 DB_S_ERRORSOCCURRED 和 DB_E_ERRORSOCCURED 之外引發。  
  
## <a name="remarks"></a>備註  
 **Getparameterinfo**方法行為一致相對於**GetParameterInfo**。 如果[isscommandwithparameters::](../../oledb/ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md)或**SetParameterInfo**尚未呼叫或呼叫 cparams 等於零， **GetParameterInfo**衍生參數資訊，並傳回它。 如果**isscommandwithparameters::** 或**SetParameterInfo**至少一個參數，在呼叫**Getparameterinfo**方法會傳回這些參數的屬性為其**isscommandwithparameters::** 已呼叫。 如果**isscommandwithparameters::** 之後呼叫**Getparameterinfo**或**GetParameterInfo**，後續呼叫**Getparameterinfo**覆寫這些參數的值傳回的**isscommandwithparameters::** 呼叫方法。  
  
 SSPARAMPROPS 結構定義如下：  
  
 `struct SSPARAMPROPS {`  
  
 `DBORDINAL iOrdinal;`  
  
 `ULONG cPropertySets;`  
  
 `DBPROPSET *rgPropertySets;`  
  
 `};`  
  
|成員|描述|  
|------------|-----------------|  
|*iOrdinal*|所傳遞參數的序數。|  
|*cPropertySets*|的 DBPROPSET 結構數目中*rgPropertySets*。|  
|*rgPropertySets*|藉其傳回 DBPROPSET 結構陣列的記憶體指標。|  
  
## <a name="see-also"></a>另請參閱  
 [ISSCommandWithParameters &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  

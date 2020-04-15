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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
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
 藉其傳回 SSPARAMPROPS 結構陣列的記憶體指標。 提供程式為結構分配記憶體,並將位址返回到此記憶體;消費者使用**IMalloc 釋放此記憶體::** 當它不再需要結構時,它是免費的。 在調用**IMalloc::對** *prgParamProperties*免費之前,消費者還必須為每個 DBPROP 結構的*vValue*屬性調用**VariantClear,** 以防止在變體包含引用類型(如 BSTR)的情況下出現記憶體洩漏。如果*pcParams*在輸出時為零或發生DB_E_ERRORSOCCURRED以外的錯誤,則提供程式不會分配任何記憶體,並確保*prgParamProperties*是輸出上的空指標。  
  
## <a name="return-code-values"></a>傳回碼值  
 **Get參數屬性**方法返回與核心 OLE DB **ICommand屬性相同的錯誤代碼::getProperties**方法,但無法引發DB_S_ERRORSOCCURRED和DB_E_ERRORSOCCURED。  
  
## <a name="remarks"></a>備註  
 **ISS命令與參數::獲取參數屬性**在**Get參數資訊**方面的行為一致。 如果[ISSCommand 與參數::設定參數屬性](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md)或**Set 參數資訊**尚未調用或已調用 cParams 等於零 **,Getparameterinfo**將派生參數資訊並返回此資訊。 如果**ISSCommand 與參數::設定參數屬性**或**設置參數資訊**已至少調用一個參數,**則 ISSCommand 與參數:get 參數屬性**僅返回已為其調用**ISSCommand 與參數::set 參數屬性**的參數的屬性。 如果**ISSCommand 與參數::set 參數屬性**在**ISSCommand 與參數::獲取參數屬性**或**Getparameterinfo**之後調用,則隨後對**ISSCommand 與參數的調用:get 參數屬性**返回已調用**ISSCommand 與參數::set 參數屬性**的參數的重寫值。  
  
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
  
  

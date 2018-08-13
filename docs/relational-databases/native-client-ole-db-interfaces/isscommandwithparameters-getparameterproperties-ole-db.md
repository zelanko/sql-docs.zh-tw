---
title: Getparameterinfo (OLE DB) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISSCommandWithParameters::GetParameterProperties (OLE DB)
apitype: COM
helpviewer_keywords:
- GetParameterProperties method
ms.assetid: 7f4cc5ea-d028-4fe5-9192-bd153ab3c26c
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: db7ff5ed9c55473283091950a5d5fee6dd5cd54f
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2018
ms.locfileid: "39533449"
---
# <a name="isscommandwithparametersgetparameterproperties-ole-db"></a>ISSCommandWithParameters::GetParameterProperties (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

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
 藉其傳回 SSPARAMPROPS 結構陣列的記憶體指標。 提供者會為結構配置記憶體，並將位址傳回給這個記憶體中;取用者釋放這個記憶體**imalloc:: Free**當它不再需要的結構。 然後再呼叫**imalloc:: Free** for *prgParamProperties*，取用者還必須呼叫**VariantClear**如*vValue*屬性若要防止記憶體流失，在變數包含參考的情況下每個 DBPROP 結構的型別 （例如 BSTR。)如果*pcParams*是零個輸出，或發生錯誤 DB_E_ERRORSOCCURRED 之外，提供者不會配置任何記憶體並確保*prgParamProperties*輸出上的 null 指標。  
  
## <a name="return-code-values"></a>傳回碼值  
 **GetParameterProperties**方法會傳回相同的錯誤碼與核心 OLE DB **icommandproperties:: Getproperties**除了 DB_S_ERRORSOCCURRED 和 DB_E_ERRORSOCCURED 之外的方法，不可為引發。  
  
## <a name="remarks"></a>備註  
 **Getparameterinfo**採取一致的行為相對於**GetParameterInfo**。 如果[isscommandwithparameters:: Setparameterproperties](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md)或是**SetParameterInfo**尚未呼叫或已經呼叫 cparams 等於零， **GetParameterInfo**衍生參數資訊並傳回此資訊。 如果**isscommandwithparameters:: Setparameterproperties**或是**SetParameterInfo**至少一個參數，呼叫**Getparameterinfo** ，會傳回這些參數的屬性**isscommandwithparameters:: Setparameterproperties**已呼叫。 如果**isscommandwithparameters:: Setparameterproperties**之後，會呼叫**Getparameterinfo**或是**GetParameterInfo**，後續呼叫**Getparameterinfo**為其傳回這些參數的覆寫的值**isscommandwithparameters:: Setparameterproperties**被呼叫。  
  
 SSPARAMPROPS 結構定義如下：  
  
 `struct SSPARAMPROPS {`  
  
 `DBORDINAL iOrdinal;`  
  
 `ULONG cPropertySets;`  
  
 `DBPROPSET *rgPropertySets;`  
  
 `};`  
  
|成員|描述|  
|------------|-----------------|  
|*iOrdinal*|所傳遞參數的序數。|  
|*cPropertySets*|*rgPropertySets* 中的 DBPROPSET 結構數目。|  
|*rgPropertySets*|藉其傳回 DBPROPSET 結構陣列的記憶體指標。|  
  
## <a name="see-also"></a>另請參閱  
 [ISSCommandWithParameters &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  

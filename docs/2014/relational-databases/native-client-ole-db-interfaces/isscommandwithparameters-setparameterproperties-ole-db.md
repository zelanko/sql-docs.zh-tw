---
title: 'Isscommandwithparameters:: Setparameterproperties (OLE DB) |Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- ISSCommandWithParameters::SetParameterProperties (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- SetParameterProperties method
ms.assetid: 4cd0281a-a2a0-43df-8e46-eb478b64cb4b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 778021ce007f0c1eac68197e0c07e2cb7b0bb001
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48096978"
---
# <a name="isscommandwithparameterssetparameterproperties-ole-db"></a>ISSCommandWithParameters::SetParameterProperties (OLE DB)
  依照序數根據每個參數來設定參數的屬性，或指定 SSPARAMPROPS 結構的陣列來設定大量參數屬性。  
  
## <a name="syntax"></a>語法  
  
```  
  
HRESULT SetParameterProperties(  
DB_UPARAMS cParams,   
SSPARAMPROPS rgParamProperties[]);  
```  
  
## <a name="arguments"></a>引數  
 *cParams*[in]  
 *rgParamProperties* 陣列中 SSPARAMPROPS 結構的數目。 如果這個數字為零，`ISSCommandWithParameters::SetParameterProperties`會刪除所有可能的任何參數，在命令中指定的屬性。  
  
 *rgParamProperties*[in]  
 要設定的 SSPARAMPROPS 結構的陣列。  
  
## <a name="return-code-values"></a>傳回碼值  
 `ISSCommandWithParameters::SetParameterProperties`方法會傳回相同的錯誤碼與核心 OLE DB **icommandproperties:: Setproperties**方法。  
  
## <a name="remarks"></a>備註  
 使用此方法設定參數屬性適用於每個參數序數，或使用單一`ISSCommandWithParameters::SetParameterProperties`從屬性陣列建立 SSPARAMPROPS 之後呼叫。  
  
 **SetParameterInfo**必須呼叫方法，然後再呼叫`ISSCommandWithParameters::SetParameterProperties`方法。 呼叫 `SetParameterProperties(0, NULL)` 會清除所有指定的參數屬性，呼叫 `SetParameterInfo(0,NULL,NULL)` 則會清除所有的參數資訊，包括任何可能與參數相關聯的屬性。  
  
 呼叫`ISSCommandWithParameters::SetParameterProperties`即可指定屬性參數而不是型別 DBTYPE_XML 或 DBTYPE_UDT 會傳回 DB_E_ERRORSOCCURRED 或 DB_S_ERRORSOCCURRED，並*dwStatus* SSPARAMPROPS 中包含的所有 DBPROPs 欄位針對具有 DBPROPSTATUS_NOTSET 的該參數。 系統會周遊 SSPARAMPROPS 中包含的每個 DBPROPSET 的 DBPROP 陣列，以偵測 DB_E_ERRORSOCCURRED 或 DB_S_ERRORSOCCURRED 所參考的是哪一個參數。  
  
 如果`ISSCommandWithParameters::SetParameterProperties`呼叫以指定的參數已尚未設定其參數資訊，使用屬性**SetParameterInfo**，提供者會傳回 E_UNEXPECTED，並出現下列錯誤訊息：  
  
 必須先針對指定的參數呼叫 SetParameterInfo 方法，然後才能呼叫 SetParameterProperties 方法。 而在設定參數屬性之前，也必須先設定參數資訊。  
  
 如果呼叫`ISSCommandWithParameters::SetParameterProperties`包含一些參數，其中已設定參數資訊，而其中的參數資訊尚未設定，某些參數 SSPARAMPROPS 屬性集的 DBPROPSET 中的 dwStatus 屬性會以 DBSTATUS_NOTSET 傳回。  
  
 SSPARAMPROPS 結構定義如下：  
  
 `struct SSPARAMPROPS {`  
  
 `DBORDINAL iOrdinal;`  
  
 `ULONG cPropertySets;`  
  
 `DBPROPSET *rgPropertySets;`  
  
 `};`  
  
 在開始 database engine 的改進[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]允許 isscommandwithparameters:: Setparameterproperties 以取得更精確的預期結果的描述。 這些更精確的結果可能不同於在舊版的 isscommandwithparameters:: Setparameterproperties 傳回的值[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如需詳細資訊，請參閱 <<c0> [ 中繼資料探索](../native-client/features/metadata-discovery.md)。  
  
|成員|描述|  
|------------|-----------------|  
|*iOrdinal*|所傳遞參數的序數。|  
|*cPropertySets*|*rgPropertySets* 中的 DBPROPSET 結構數目。|  
|*rgPropertySets*|藉其傳回 DBPROPSET 結構陣列的記憶體指標。|  
  
## <a name="see-also"></a>另請參閱  
 [ISSCommandWithParameters &#40;OLE DB&#41;](isscommandwithparameters-ole-db.md)  
  
  

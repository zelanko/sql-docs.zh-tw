---
title: 'ISSCommandWithParameters:: SetParameterProperties (OLE DB) |Microsoft Docs'
description: ISSCommandWithParameters::SetParameterProperties (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- ISSCommandWithParameters::SetParameterProperties (OLE DB)
apitype: COM
helpviewer_keywords:
- SetParameterProperties method
author: pmasl
ms.author: pelopes
ms.openlocfilehash: b9f5a3251b05453d01b2ef984c6a9ea7bde1c115
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015378"
---
# <a name="isscommandwithparameterssetparameterproperties-ole-db"></a>ISSCommandWithParameters::SetParameterProperties (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  依照序數根據每個參數來設定參數的屬性，或指定 SSPARAMPROPS 結構的陣列來設定大量參數屬性。  
  
## <a name="syntax"></a>語法  
  
```  
  
HRESULT SetParameterProperties(  
      DB_UPARAMS cParams,   
      SSPARAMPROPS rgParamProperties[]);  
```  
  
## <a name="arguments"></a>引數  
 *cParams*[in]  
 *rgParamProperties* 陣列中 SSPARAMPROPS 結構的數目。 如果這個數目為零，則 **ISSCommandWithParameters::SetParameterProperties** 會刪除可能已針對命令中的任何參數所指定的所有屬性。  
  
 *rgParamProperties*[in]  
 要設定的 SSPARAMPROPS 結構的陣列。  
  
## <a name="return-code-values"></a>傳回碼值  
 **ISSCommandWithParameters::SetParameterProperties** 方法所傳回的錯誤碼與核心 OLE DB **ICommandProperties::SetProperties** 方法相同。  
  
## <a name="remarks"></a>Remarks  
 您可以依序數按照每個參數使用這個方法來設定參數屬性，或在從屬性陣列建立 SSPARAMPROPS 之後，使用單一的 **ISSCommandWithParameters::SetParameterProperties** 呼叫來設定參數屬性。  
  
 在呼叫 **ISSCommandWithParameters::SetParameterProperties** 方法之前，必須先呼叫 **SetParameterInfo** 方法。 呼叫 `SetParameterProperties(0, NULL)` 會清除所有指定的參數屬性，呼叫 `SetParameterInfo(0,NULL,NULL)` 則會清除所有的參數資訊，包括任何可能與參數相關聯的屬性。  
  
 如果呼叫 **ISSCommandWithParameters::SetParameterProperties** 以針對並非 DBTYPE_XML 或 DBTYPE_UDT 類型的參數指定屬性，便會傳回 DB_E_ERRORSOCCURRED 或 DB_S_ERRORSOCCURRED，並針對具有 DBPROPSTATUS_NOTSET 的該參數標示出包含在 SSPARAMPROPS 中所有 DBPROP 的 *dwStatus* 欄位。 系統會周遊 SSPARAMPROPS 中包含的每個 DBPROPSET 的 DBPROP 陣列，以偵測 DB_E_ERRORSOCCURRED 或 DB_S_ERRORSOCCURRED 所參考的是哪一個參數。  
  
 如果呼叫 **ISSCommandWithParameters::SetParameterProperties** 來指定參數 (尚未使用 **SetParameterInfo** 設定其參數資訊) 的屬性，則提供者會傳回 E_UNEXPECTED 且顯示下列錯誤訊息：  
  
 必須先針對指定的參數呼叫 SetParameterInfo 方法，然後才能呼叫 SetParameterProperties 方法。 而在設定參數屬性之前，也必須先設定參數資訊。  
  
 如果 **ISSCommandWithParameters::SetParameterProperties** 的呼叫所包含的參數中有些已設定參數資訊，有些尚未設定，則 SSPARAMPROPS 屬性集的 DBPROPSET 中的 dwStatus 屬性會以 DBSTATUS_NOTSET 傳回。  
  
 SSPARAMPROPS 結構定義如下：  
  
 `struct SSPARAMPROPS {`  
  
 `DBORDINAL iOrdinal;`  
  
 `ULONG cPropertySets;`  
  
 `DBPROPSET *rgPropertySets;`  
  
 `};`  
  
 資料庫引擎的改良功能從[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]允許 ISSCommandWithParameters:: SetParameterProperties 開始, 以取得更精確的預期結果描述。 這些更精確的結果可能與舊版的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]ISSCommandWithParameters:: SetParameterProperties 所傳回的值不同。 如需詳細資訊, 請參閱[中繼資料探索](../../oledb/features/metadata-discovery.md)。  
  
|成員|Description|  
|------------|-----------------|  
|*iOrdinal*|所傳遞參數的序數。|  
|*cPropertySets*|*rgPropertySets* 中的 DBPROPSET 結構數目。|  
|*rgPropertySets*|藉其傳回 DBPROPSET 結構陣列的記憶體指標。|  
  
## <a name="see-also"></a>另請參閱  
 [ISSCommandWithParameters &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  

---
title: CommandTypeEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CommandTypeEnum
helpviewer_keywords:
- CommandTypeEnum enumeration [ADO]
ms.assetid: 4b1feb9c-a855-40fe-a906-efe688687e9f
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 09874df6d9e09da8b6dc0df3e9670e4ff130c511
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66695974"
---
# <a name="commandtypeenum"></a>CommandTypeEnum
指定應該如何解譯為命令引數。  
  
 請務必驗證使用者提供*CommandString*值，以避免讓應用程式使用者有機會將用於 ADO 來執行有潛在危險的命令。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adCmdUnspecified**|-1|未指定命令的型別引數。|  
|**adCmdText**|1|會評估[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)做為文字定義命令或預存程序的呼叫。|  
|**adCmdTable**|2|會評估**CommandText**資料表的名稱，其資料行都會傳回內部產生的 SQL 查詢。|  
|**adCmdStoredProc**|4|會評估**CommandText**做為預存程序名稱。|  
|**adCmdUnknown**|8|預設值。 表示命令中的類型**CommandText**並不知道屬性。<br /><br /> 當命令的類型未知時，ADO 會多次嘗試才能解譯**CommandText**。<br /><br /> -   **CommandText**會解譯為文字定義命令或預存程序呼叫。 這是相同的行為**adCmdText**。<br />-   **CommandText**是預存程序的名稱。 這是相同的行為**adCmdStoredProc**。<br />-   **CommandText**會解譯為資料表的名稱。 內部產生的 SQL 查詢會傳回所有資料行。 這是相同的行為**adCmdTable**。|  
|**adCmdFile**|256|會評估**CommandText**持續預存的檔案名稱作為[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。 搭配**資料錄集。** [開放](../../../ado/reference/ado-api/open-method-ado-recordset.md)或是[Requery](../../../ado/reference/ado-api/requery-method.md)只。|  
|**adCmdTableDirect**|512|會評估**CommandText**都會傳回的資料行資料表的名稱。 搭配**Recordset.Open**或是**Requery**只。 若要使用[Seek](../../../ado/reference/ado-api/seek-method.md)方法， **Recordset**必須以開啟**adCmdTableDirect**。<br /><br /> 此值不得搭配[的執行方式](../../../ado/reference/ado-api/executeoptionenum.md)值**adAsyncExecute**。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 封裝： **com.ms.wfc.data**  
  
|常數|  
|--------------|  
|AdoEnums.CommandType.UNSPECIFIED|  
|AdoEnums.CommandType.TEXT|  
|AdoEnums.CommandType.TABLE|  
|AdoEnums.CommandType.STOREDPROC|  
|AdoEnums.CommandType.UNKNOWN|  
|AdoEnums.CommandType.FILE|  
|AdoEnums.CommandType.TABLEDIRECT|  
  
## <a name="applies-to"></a>適用於  
  
|||  
|-|-|  
|[CommandType 屬性 (ADO)](../../../ado/reference/ado-api/commandtype-property-ado.md)|[Execute 方法 (ADO Command)](../../../ado/reference/ado-api/execute-method-ado-command.md)|  
|[Execute 方法 (ADO Connection)](../../../ado/reference/ado-api/execute-method-ado-connection.md)|[Open 方法 (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)|  
|[Requery 方法](../../../ado/reference/ado-api/requery-method.md)||

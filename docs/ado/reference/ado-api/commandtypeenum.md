---
title: "CommandTypeEnum |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: CommandTypeEnum
helpviewer_keywords: CommandTypeEnum enumeration [ADO]
ms.assetid: 4b1feb9c-a855-40fe-a906-efe688687e9f
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: fb7c01971633727f1e7e5769060b256eab13914b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="commandtypeenum"></a>CommandTypeEnum
指定應如何解譯為命令引數。  
  
 請務必驗證使用者提供*CommandString*值，以免讓應用程式使用者有機會將用於 ADO 來執行有潛在危險的命令。  
  
|常數|ReplTest1|描述|  
|--------------|-----------|-----------------|  
|**adCmdUnspecified**|-1|未指定命令的型別引數。|  
|**adCmdText**|@shouldalert|評估[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)做為文字定義命令或預存程序的呼叫。|  
|**adCmdTable**|2|評估**CommandText**做為其資料行大小會傳回由內部產生的 SQL 查詢的資料表名稱。|  
|**adCmdStoredProc**|4|評估**CommandText**做為預存程序名稱。|  
|**adCmdUnknown**|8|預設值。 表示命令中的型別**CommandText**並不知道屬性。<br /><br /> ADO 在不知道的命令類型，也必須用於解譯多嘗試幾次**CommandText**。<br /><br /> -   **CommandText**解譯為文字的命令或預存程序呼叫的定義。 這是相同的行為**adCmdText**。<br />-   **CommandText**是預存程序的名稱。 這是相同的行為**adCmdStoredProc**。<br />-   **CommandText**解譯為資料表的名稱。 由內部產生的 SQL 查詢會傳回所有資料行。 這是相同的行為**adCmdTable**。|  
|**adCmdFile**|256|評估**CommandText**持續預存的檔案名稱作為[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。 搭配**資料錄集。**[開啟](../../../ado/reference/ado-api/open-method-ado-recordset.md)或[Requery](../../../ado/reference/ado-api/requery-method.md)只。|  
|**adCmdTableDirect**|512|評估**CommandText**做為所有傳回的資料行的資料表名稱。 搭配**Recordset.Open**或**Requery**只。 若要使用[搜尋](../../../ado/reference/ado-api/seek-method.md)方法，**資料錄集**必須以開啟**adCmdTableDirect**。<br /><br /> 此值不能與結合[的執行方式](../../../ado/reference/ado-api/executeoptionenum.md)值**adAsyncExecute**。|  
  
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

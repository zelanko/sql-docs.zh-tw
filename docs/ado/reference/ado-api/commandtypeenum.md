---
description: CommandTypeEnum
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 994fe5eb0cf10189477e11154b8814f5e73c9194
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776077"
---
# <a name="commandtypeenum"></a>CommandTypeEnum
指定如何解讀命令引數。  
  
 請務必驗證使用者提供的 *CommandString* 值，以避免讓應用程式使用者有機會插入可能有危險的 ADO 執行命令。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adCmdUnspecified**|-1|未指定命令類型引數。|  
|**adCmdText**|1|評估 [CommandText](./commandtext-property-ado.md) 為命令或預存程序呼叫的文字定義。|  
|**adCmdTable**|2|將 **CommandText** 評估為數據表名稱，其資料行全都由內部產生的 SQL 查詢傳回。|  
|**adCmdStoredProc**|4|評估 **CommandText** 是否為預存程式名稱。|  
|**adCmdUnknown**|8|預設值。 指出 **CommandText** 屬性中的命令類型未知。<br /><br /> 當未知的命令類型時，ADO 將會進行數次解讀 **CommandText**的嘗試。<br /><br /> -   **CommandText** 會被視為命令或預存程序呼叫的文字定義。 這與 **adCmdText**的行為相同。<br />-   **CommandText** 是預存程式的名稱。 這與 **adCmdStoredProc**的行為相同。<br />-   **CommandText** 會被解釋為數據表的名稱。 內部產生的 SQL 查詢會傳回所有資料行。 這與 **adCmdTable**的行為相同。|  
|**adCmdFile**|256|將 **CommandText** 評估為持續儲存之 [記錄集](./recordset-object-ado.md)的檔案名。 與**記錄集**一起使用。只[開啟](./open-method-ado-recordset.md)或重新[查詢](./requery-method.md)。|  
|**adCmdTableDirect**|512|將 **CommandText** 評估為數據表名稱，其資料行全都會傳回。 與 **記錄集** 一起使用。請只開啟或重新 **查詢** 。 若要使用[Seek](./seek-method.md)方法，必須以**AdCmdTableDirect**開啟**記錄集**。<br /><br /> 此值無法與 [ExecuteOptionEnum](./executeoptionenum.md) 值 **adAsyncExecute**結合。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 相等  
 封裝： **.com. 資料**  
  
|持續性|  
|--------------|  
|AdoEnums. CommandType。未指定|  
|AdoEnums. CommandType. TEXT|  
|AdoEnums. CommandType 資料表|  
|AdoEnums. CommandType. STOREDPROC|  
|AdoEnums. CommandType。未知|  
|AdoEnums. CommandType. FILE|  
|AdoEnums. CommandType. TABLEDIRECT|  
  
## <a name="applies-to"></a>套用至  

:::row:::
    :::column:::
        [CommandType 屬性 (ADO)](./commandtype-property-ado.md)  
        [Execute 方法 (ADO 命令)](./execute-method-ado-command.md)  
    :::column-end:::
    :::column:::
        [Execute 方法 (ADO Connection)](./execute-method-ado-connection.md)  
        [Open 方法 (ADO Recordset)](./open-method-ado-recordset.md)  
    :::column-end:::
    :::column:::
        [Requery 方法](./requery-method.md)  
    :::column-end:::
:::row-end:::
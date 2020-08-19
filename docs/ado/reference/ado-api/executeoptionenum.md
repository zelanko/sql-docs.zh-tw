---
description: ExecuteOptionEnum
title: ExecuteOptionEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ExecuteOptionEnum
helpviewer_keywords:
- ExecuteOptionEnum enumeration [ADO]
ms.assetid: 68bfa83a-5df4-4bef-8736-0f88ae8c29ea
author: rothja
ms.author: jroth
ms.openlocfilehash: 4ab70f52adb11d1b242dd0f1bbce11bea221ed55
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443830"
---
# <a name="executeoptionenum"></a>ExecuteOptionEnum
指定提供者應該如何執行命令。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adAsyncExecute**|0x10|指出命令應該以非同步方式執行。<br /><br /> 此值無法與 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) 值 **adCmdTableDirect**結合。|  
|**adAsyncFetch**|0x20|表示應該以非同步方式抓取 [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md) 屬性中指定的初始數量之後的其餘資料列。|  
|**adAsyncFetchNonBlocking**|0x40|表示主執行緒在抓取時永遠不會封鎖。 如果未抓取要求的資料列，則目前的資料列會自動移至檔案結尾。<br /><br /> 如果您從包含持續儲存之**記錄集**的[資料流程](../../../ado/reference/ado-api/stream-object-ado.md)開啟[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)， **adAsyncFetchNonBlocking**將不會有任何作用;作業將會是同步和封鎖。<br /><br /> 當使用[adCmdTableDirect](../../../ado/reference/ado-api/commandtypeenum.md)選項來開啟**記錄集**時， **adAsynchFetchNonBlocking**不會有任何作用。|  
|**adExecuteNoRecords**|0x80|指出命令文字是不會傳回資料列的命令或預存程式 (例如，只插入資料) 的命令。 如果有抓取任何資料列，則會捨棄這些資料列，而且不會傳回。<br /><br /> **adExecuteNoRecords** 只能做為選擇性參數傳遞至 **命令** 或 **連接執行** 方法。|  
|**adExecuteStream**|0x400|表示命令執行的結果應該以資料流程的形式傳回。<br /><br /> **adExecuteStream** 只能做為選擇性參數傳遞至 **命令 Execute** 方法。|  
|**adExecuteRecord**||指出 **CommandText** 是一個命令或預存程式，它會傳回應以 **記錄** 物件形式傳回的單一資料列。|  
|**adOptionUnspecified**|-1|指出未指定命令。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 相等  
 封裝： **.com. 資料**  
  
|常數|  
|--------------|  
|AdoEnums.ExecuteOption. ASYNCEXECUTE|  
|AdoEnums.ExecuteOption. ASYNCFETCH|  
|AdoEnums.ExecuteOption. ASYNCFETCHNONBLOCKING|  
|AdoEnums.ExecuteOption. NORECORDS|  
|AdoEnums.ExecuteOption 未指定|  
  
## <a name="applies-to"></a>套用至  

:::row:::
    :::column:::
        [Execute 方法 (ADO 命令)](../../../ado/reference/ado-api/execute-method-ado-command.md)  
        [Execute 方法 (ADO Connection)](../../../ado/reference/ado-api/execute-method-ado-connection.md)  
    :::column-end:::
    :::column:::
        [Open 方法 (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)  
        [Requery 方法](../../../ado/reference/ado-api/requery-method.md)  
    :::column-end:::
:::row-end:::

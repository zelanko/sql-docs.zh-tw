---
title: "執行方式 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: ExecuteOptionEnum
helpviewer_keywords: ExecuteOptionEnum enumeration [ADO]
ms.assetid: 68bfa83a-5df4-4bef-8736-0f88ae8c29ea
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8357988f5082498114c435f899e898552fca1707
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="executeoptionenum"></a>執行方式
指定提供者如何執行命令。  
  
|常數|值|Description|  
|--------------|-----------|-----------------|  
|**adAsyncExecute**|0x10|表示命令應該以非同步方式執行。<br /><br /> 此值不能與結合[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)值**adCmdTableDirect**。|  
|**adAsyncFetch**|0x20|指示的其餘資料列中指定的初始的數量之後[CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)應該以非同步方式擷取屬性。|  
|**adAsyncFetchNonBlocking**|0x40|表示在擷取時，永遠不會封鎖主執行緒。 如果尚未擷取要求的資料列，目前的資料列會自動移至檔案結尾。<br /><br /> 如果您開啟[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)從[資料流](../../../ado/reference/ado-api/stream-object-ado.md)包含持續預存**資料錄集**， **adAsyncFetchNonBlocking**不會有效果;作業會同步和封鎖。<br /><br /> **adAsynchFetchNonBlocking**沒有任何作用[adCmdTableDirect](../../../ado/reference/ado-api/commandtypeenum.md)選項用來開啟**資料錄集**。|  
|**adExecuteNoRecords**|0x80|表示命令文字的命令或預存程序不會傳回資料列 （例如，只將資料插入命令）。 如果擷取任何資料列，它們捨棄而且不會傳回。<br /><br /> **adExecuteNoRecords**只能做為選擇性參數來傳遞**命令**或**連線執行**方法。|  
|**adExecuteStream**|0x400|指出應傳回做為資料流的命令執行的結果。<br /><br /> **adExecuteStream**只能做為選擇性參數來傳遞**命令執行**方法。|  
|**adExecuteRecord**||表示**CommandText**命令或預存程序傳回單一資料列都應該以傳回**記錄**物件。|  
|**adOptionUnspecified**|-1|表示未指定命令。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 封裝： **com.ms.wfc.data**  
  
|常數|  
|--------------|  
|AdoEnums.ExecuteOption.ASYNCEXECUTE|  
|AdoEnums.ExecuteOption.ASYNCFETCH|  
|AdoEnums.ExecuteOption.ASYNCFETCHNONBLOCKING|  
|AdoEnums.ExecuteOption.NORECORDS|  
|AdoEnums.ExecuteOption.UNSPECIFIED|  
  
## <a name="applies-to"></a>適用於  
  
|||  
|-|-|  
|[Execute 方法 (ADO Command)](../../../ado/reference/ado-api/execute-method-ado-command.md)|[Execute 方法 (ADO Connection)](../../../ado/reference/ado-api/execute-method-ado-connection.md)|  
|[Open 方法 (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)|[Requery 方法](../../../ado/reference/ado-api/requery-method.md)|

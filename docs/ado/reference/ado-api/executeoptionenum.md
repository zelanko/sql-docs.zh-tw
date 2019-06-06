---
title: ExecuteOptionEnum | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 589519e7c4a075d5fb06b5f2640d48e5d4ed898d
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66695269"
---
# <a name="executeoptionenum"></a>ExecuteOptionEnum
指定提供者執行命令的方式。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adAsyncExecute**|0x10|指出命令應該以非同步方式執行。<br /><br /> 此值不得搭配[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)值**adCmdTableDirect**。|  
|**adAsyncFetch**|0x20|指示的其餘資料列中指定的初始數量之後[CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)應該以非同步方式擷取屬性。|  
|**adAsyncFetchNonBlocking**|0x40|指出在擷取時，永遠不會封鎖主執行緒。 如果尚未擷取要求的資料列，目前的資料列會自動移至檔案結尾。<br /><br /> 如果您開啟[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)從[Stream](../../../ado/reference/ado-api/stream-object-ado.md)包含持續預存**資料錄集**， **adAsyncFetchNonBlocking**不會影響;作業會同步和封鎖。<br /><br /> **adAsynchFetchNonBlocking**沒有時生效[adCmdTableDirect](../../../ado/reference/ado-api/commandtypeenum.md)選項用來開啟**資料錄集**。|  
|**adExecuteNoRecords**|0x80|表示命令文字的命令或預存程序不會傳回資料列 （例如，只將資料插入命令）。 如果擷取任何資料列，它們會被捨棄，不會傳回。<br /><br /> **adExecuteNoRecords**只能為選擇性的參數，以傳遞**命令**或是**連線執行**方法。|  
|**adExecuteStream**|0x400|表示代表命令執行的結果不應傳回做為資料流。<br /><br /> **adExecuteStream**只能為選擇性的參數，以傳遞**Command Execute**方法。|  
|**adExecuteRecord**||指出**CommandText**是命令或預存程序傳回單一資料列應該做為傳回**記錄**物件。|  
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

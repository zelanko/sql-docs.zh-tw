---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bef70bd72425e749865e31ecf162e719737dd272
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67932849"
---
# <a name="executeoptionenum"></a>ExecuteOptionEnum
指定提供者應該如何執行命令。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adAsyncExecute**|0x10|指出命令應該以非同步方式執行。<br /><br /> 這個值無法與[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)值**adCmdTableDirect**結合。|  
|**adAsyncFetch**|0x20|表示在[CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)屬性中指定的初始數量之後，其餘的資料列應以非同步方式抓取。|  
|**adAsyncFetchNonBlocking**|0x40|表示在抓取時，主執行緒永遠不會封鎖。 如果未抓取要求的資料列，則目前的資料列會自動移至檔案結尾。<br /><br /> 如果您從包含持續儲存之**記錄集**的[資料流程](../../../ado/reference/ado-api/stream-object-ado.md)開啟[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)， **adAsyncFetchNonBlocking**將不會有任何作用;作業將會同步並封鎖。<br /><br /> 當[adCmdTableDirect](../../../ado/reference/ado-api/commandtypeenum.md)選項用來開啟**記錄集**時， **adAsynchFetchNonBlocking**沒有作用。|  
|**adExecuteNoRecords**|0x80|指出命令文字是不會傳回資料列的命令或預存程式（例如，只會插入資料的命令）。 如果取得任何資料列，則會將其捨棄且不會傳回。<br /><br /> **adExecuteNoRecords**只能當做選擇性參數傳遞至**命令**或**連接執行**方法。|  
|**adExecuteStream**|0x400|指出應以資料流程的形式傳回命令執行的結果。<br /><br /> **adExecuteStream**只能以選擇性參數的形式傳遞至**命令執行**方法。|  
|**adExecuteRecord**||指出**CommandText**是一個命令或預存程式，它會傳回單一資料列，而該資料列應以**記錄**物件的形式傳回。|  
|**adOptionUnspecified**|-1|表示未指定命令。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等  
 Package： **.com. wfc. 資料**  
  
|持續性|  
|--------------|  
|AdoEnums.ExecuteOption.ASYNCEXECUTE|  
|AdoEnums.ExecuteOption.ASYNCFETCH|  
|AdoEnums.ExecuteOption.ASYNCFETCHNONBLOCKING|  
|AdoEnums.ExecuteOption.NORECORDS|  
|AdoEnums. ExecuteOption。未指定|  
  
## <a name="applies-to"></a>套用至  
  
|||  
|-|-|  
|[Execute 方法 (ADO 命令)](../../../ado/reference/ado-api/execute-method-ado-command.md)|[Execute 方法 (ADO Connection)](../../../ado/reference/ado-api/execute-method-ado-connection.md)|  
|[Open 方法 (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)|[Requery 方法](../../../ado/reference/ado-api/requery-method.md)|

---
description: IsolationLevelEnum
title: IsolationLevelEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- IsolationLevelEnum
helpviewer_keywords:
- IsolationLevelEnum enumeration [ADO]
ms.assetid: 8e17a7bc-b8a3-4ae2-b6c9-ce088ad31fdf
author: rothja
ms.author: jroth
ms.openlocfilehash: 0c08da68e136d3e2cffbb492f021225a3b895a9e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443410"
---
# <a name="isolationlevelenum"></a>IsolationLevelEnum
指定 [連接](../../../ado/reference/ado-api/connection-object-ado.md) 物件的交易隔離層級。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adXactUnspecified**|-1|表示提供者所使用的隔離等級與指定的不同，但無法判斷層級。|  
|**adXactChaos**|16|表示無法覆寫來自更高隔離交易的暫止變更。|  
|**adXactBrowse**|256|表示從某個交易中，您可以在其他交易中查看未認可的變更。|  
|**adXactReadUncommitted**|256|與 **adXactBrowse**相同。|  
|**adXactCursorStability**|4096|表示從某個交易中，您只能在認可之前查看其他交易中的變更。|  
|**adXactReadCommitted**|4096|與 **adXactCursorStability**相同。|  
|**adXactRepeatableRead**|65536|表示從某個交易中，您看不到在其他交易中所做的變更，但是重新查詢可能會取得新的 **記錄集** 物件。|  
|**adXactIsolated**|1048576|指出交易會與其他交易隔離。|  
|**adXactSerializable**|1048576|與 **adXactIsolated**相同。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 相等  
 封裝： **.com. 資料**  
  
|常數|  
|--------------|  
|AdoEnums. IsolationLevel。未指定|  
|AdoEnums. IsolationLevel|  
|AdoEnums. IsolationLevel. 流覽|  
|AdoEnums. IsolationLevel. READUNCOMMITTED|  
|AdoEnums. IsolationLevel. CURSORSTABILITY|  
|AdoEnums. IsolationLevel. READCOMMITTED|  
|AdoEnums. IsolationLevel. REPEATABLEREAD|  
|AdoEnums. IsolationLevel 獨立模式|  
|AdoEnums. IsolationLevel SERIALIZABLE|  
  
## <a name="applies-to"></a>套用至  
 [IsolationLevel 屬性](../../../ado/reference/ado-api/isolationlevel-property.md)

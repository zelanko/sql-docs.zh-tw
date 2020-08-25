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
ms.openlocfilehash: 03bd95a642f3942275e1ff9d32f1b2d1829b96d3
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88774687"
---
# <a name="isolationlevelenum"></a>IsolationLevelEnum
指定 [連接](./connection-object-ado.md) 物件的交易隔離層級。  
  
|持續性|值|描述|  
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
  
|持續性|  
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
 [IsolationLevel 屬性](./isolationlevel-property.md)
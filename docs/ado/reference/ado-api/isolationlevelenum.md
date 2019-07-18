---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 15ae2aac2851c496b6cac9e47d37fe5fa26b8e34
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67918368"
---
# <a name="isolationlevelenum"></a>IsolationLevelEnum
指定的交易隔離層級[連線](../../../ado/reference/ado-api/connection-object-ado.md)物件。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adXactUnspecified**|-1|表示提供者會使用不同的隔離等級，比指定，但無法判斷層級。|  
|**adXactChaos**|16|表示暫止的變更從隔離程度更深的交易不會覆寫。|  
|**adXactBrowse**|256|指出，從某個交易您可以檢視未認可的變更在其他交易中。|  
|**adXactReadUncommitted**|256|與相同**adXactBrowse**。|  
|**adXactCursorStability**|4096|指出，從某個交易您可以檢視變更在其他交易已認可之後，才。|  
|**adXactReadCommitted**|4096|與相同**adXactCursorStability**。|  
|**adXactRepeatableRead**|65536|表示從某個交易中，您無法看到在其他交易中，所做的變更，但該重新查詢可以擷取新**資料錄集**物件。|  
|**adXactIsolated**|1048576|指出交易進行中的其他交易隔離。|  
|**adXactSerializable**|1048576|與相同**adXactIsolated**。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 封裝： **com.ms.wfc.data**  
  
|常數|  
|--------------|  
|AdoEnums.IsolationLevel.UNSPECIFIED|  
|AdoEnums.IsolationLevel.CHAOS|  
|AdoEnums.IsolationLevel.BROWSE|  
|AdoEnums.IsolationLevel.READUNCOMMITTED|  
|AdoEnums.IsolationLevel.CURSORSTABILITY|  
|AdoEnums.IsolationLevel.READCOMMITTED|  
|AdoEnums.IsolationLevel.REPEATABLEREAD|  
|AdoEnums.IsolationLevel.ISOLATED|  
|AdoEnums.IsolationLevel.SERIALIZABLE|  
  
## <a name="applies-to"></a>適用於  
 [IsolationLevel 屬性](../../../ado/reference/ado-api/isolationlevel-property.md)

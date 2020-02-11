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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67918368"
---
# <a name="isolationlevelenum"></a>IsolationLevelEnum
指定[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件的交易隔離層級。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adXactUnspecified**|-1|指出提供者所使用的隔離等級與指定的不同，但無法判斷層級。|  
|**adXactChaos**|16|表示無法覆寫來自較高隔離交易的暫止變更。|  
|**adXactBrowse**|256|表示您可以從一個交易中，查看其他交易中未認可的變更。|  
|**adXactReadUncommitted**|256|與**adXactBrowse**相同。|  
|**adXactCursorStability**|4096|表示您可以從一個交易中，只在認可之後，才查看其他交易中的變更。|  
|**adXactReadCommitted**|4096|與**adXactCursorStability**相同。|  
|**adXactRepeatableRead**|65536|表示在某個交易中，您看不到在其他交易中所做的變更，但是重新查詢可以抓取新的**記錄集**物件。|  
|**adXactIsolated**|1048576|表示交易會隔離其他交易。|  
|**adXactSerializable**|1048576|與**adXactIsolated**相同。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等  
 Package： **.com. wfc. 資料**  
  
|持續性|  
|--------------|  
|AdoEnums. IsolationLevel。未指定|  
|AdoEnums. IsolationLevel。混亂|  
|AdoEnums. IsolationLevel. 流覽|  
|AdoEnums. IsolationLevel. READUNCOMMITTED|  
|AdoEnums. IsolationLevel. CURSORSTABILITY|  
|AdoEnums. IsolationLevel. READCOMMITTED|  
|AdoEnums. IsolationLevel. REPEATABLEREAD|  
|AdoEnums. IsolationLevel. 獨立模式|  
|AdoEnums. IsolationLevel。 SERIALIZABLE|  
  
## <a name="applies-to"></a>套用至  
 [IsolationLevel 屬性](../../../ado/reference/ado-api/isolationlevel-property.md)

---
title: "IsolationLevelEnum |Microsoft 文件"
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
f1_keywords: IsolationLevelEnum
helpviewer_keywords: IsolationLevelEnum enumeration [ADO]
ms.assetid: 8e17a7bc-b8a3-4ae2-b6c9-ce088ad31fdf
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 81659537335129e820a5bc610e05fce2d2bca081
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="isolationlevelenum"></a>IsolationLevelEnum
指定的交易隔離層級[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件。  
  
|常數|ReplTest1|描述|  
|--------------|-----------|-----------------|  
|**adXactUnspecified**|-1|表示提供者會使用不同的隔離等級比指定，但無法判斷層級。|  
|**adXactChaos**|16|表示暫止的變更，更高隔離性的交易不會覆寫。|  
|**adXactBrowse**|256|表示，從某個交易您可以檢視未認可的變更在其他交易中。|  
|**adXactReadUncommitted**|256|與相同**adXactBrowse**。|  
|**adXactCursorStability**|4096|表示，從某個交易您可以檢視變更在其他交易已認可之後，才。|  
|**adXactReadCommitted**|4096|與相同**adXactCursorStability**。|  
|**adXactRepeatableRead**|65536|表示從某個交易中，您無法看到在其他交易中，所做的變更，但是該查詢可以擷取新**資料錄集**物件。|  
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

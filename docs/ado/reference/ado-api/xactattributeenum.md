---
description: XactAttributeEnum
title: XactAttributeEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- XactAttributeEnum
helpviewer_keywords:
- XactAttributeEnum enumeration [ADO]
ms.assetid: e7dcecd3-7dc7-445c-b922-f700c3067fbc
author: rothja
ms.author: jroth
ms.openlocfilehash: bb2a1391e813fd80c394bd685eff07e06015dd5b
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88987689"
---
# <a name="xactattributeenum"></a>XactAttributeEnum
指定 [連接](./connection-object-ado.md) 物件的交易屬性。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adXactAbortRetaining**|262144|藉由呼叫 [RollbackTrans](./begintrans-committrans-and-rollbacktrans-methods-ado.md) 來自動啟動新的交易，以執行保留中止。 並非所有提供者都支援此行為。|  
|**adXactCommitRetaining**|131072|藉由呼叫 [CommitTrans](./begintrans-committrans-and-rollbacktrans-methods-ado.md) 來自動啟動新的交易，以執行保留認可。 並非所有提供者都支援此行為。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 相等  
 封裝： **.com. 資料**  
  
|持續性|  
|--------------|  
|AdoEnums.XactAttribute.ABORTRETAINING|  
|AdoEnums.XactAttribute.COMMITRETAINING|  
  
## <a name="applies-to"></a>套用至  
 [Attributes 屬性 (ADO)](./attributes-property-ado.md)
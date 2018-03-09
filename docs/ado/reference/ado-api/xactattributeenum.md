---
title: XactAttributeEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- XactAttributeEnum
helpviewer_keywords:
- XactAttributeEnum enumeration [ADO]
ms.assetid: e7dcecd3-7dc7-445c-b922-f700c3067fbc
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c4ffc6f7ad1c7b65a5a6345c459c695409840a1e
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="xactattributeenum"></a>XactAttributeEnum
指定的交易屬性[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件。  
  
|常數|Value|Description|  
|--------------|-----------|-----------------|  
|**adXactAbortRetaining**|262144|藉由呼叫執行保留中止[RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)自動啟動新交易。 並非所有提供者支援這個行為。|  
|**adXactCommitRetaining**|131072|會保留認可執行藉由呼叫[CommitTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)自動啟動新交易。 並非所有提供者支援這個行為。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 Package: **com.ms.wfc.data**  
  
|常數|  
|--------------|  
|AdoEnums.XactAttribute.ABORTRETAINING|  
|AdoEnums.XactAttribute.COMMITRETAINING|  
  
## <a name="applies-to"></a>適用於  
 [Attributes 屬性 (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)

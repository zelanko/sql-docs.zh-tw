---
title: XactAttributeEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d828c2b9b49138cc4dfd6345d90e70c333554fe0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67947436"
---
# <a name="xactattributeenum"></a>XactAttributeEnum
指定[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件的交易屬性。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adXactAbortRetaining**|262144|藉由呼叫[RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)來自動啟動新的交易，以執行保留中止。 並非所有提供者都支援此行為。|  
|**adXactCommitRetaining**|131072|藉由呼叫[CommitTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)來自動啟動新的交易，藉以執行保留的認可。 並非所有提供者都支援此行為。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等  
 Package： **.com. wfc. 資料**  
  
|持續性|  
|--------------|  
|AdoEnums.XactAttribute.ABORTRETAINING|  
|AdoEnums.XactAttribute.COMMITRETAINING|  
  
## <a name="applies-to"></a>套用至  
 [Attributes 屬性 (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)

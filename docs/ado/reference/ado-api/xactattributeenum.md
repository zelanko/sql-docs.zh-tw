---
description: XactAttributeEnum
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 2528c9b7a8cf9eb2918983d90e57ac39e6ee989e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441450"
---
# <a name="xactattributeenum"></a>XactAttributeEnum
指定 [連接](../../../ado/reference/ado-api/connection-object-ado.md) 物件的交易屬性。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adXactAbortRetaining**|262144|藉由呼叫 [RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) 來自動啟動新的交易，以執行保留中止。 並非所有提供者都支援此行為。|  
|**adXactCommitRetaining**|131072|藉由呼叫 [CommitTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) 來自動啟動新的交易，以執行保留認可。 並非所有提供者都支援此行為。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 相等  
 封裝： **.com. 資料**  
  
|常數|  
|--------------|  
|AdoEnums.XactAttribute.ABORTRETAINING|  
|AdoEnums.XactAttribute.COMMITRETAINING|  
  
## <a name="applies-to"></a>套用至  
 [Attributes 屬性 (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)

---
description: ConnectOptionEnum
title: ConnectOptionEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ConnectOptionEnum
helpviewer_keywords:
- ConnectOptionEnum enumeration [ADO]
ms.assetid: bff07eeb-dee3-4e4e-9b2d-d56061ea744d
author: rothja
ms.author: jroth
ms.openlocfilehash: b924acf0f41ead3025197bade8bcc2d459508f2a
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88974689"
---
# <a name="connectoptionenum"></a>ConnectOptionEnum
指定在建立連接之後，[連接](./connection-object-ado.md)物件的[開啟](./open-method-ado-connection.md)方法是否應該傳回 (同步) 或在 (非同步) 之前傳回。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adAsyncConnect**|16|以非同步方式開啟連接。 [ConnectComplete](./connectcomplete-and-disconnect-events-ado.md)事件可以用來判斷連接何時可用。|  
|**adConnectUnspecified**|-1|預設值。 以同步方式開啟連接。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 相等  
 封裝： **.com. 資料**  
  
|持續性|  
|--------------|  
|AdoEnums.ConnectOption.ASYNCCONNECT|  
|AdoEnums.ConnectOption.CONNECTUNSPECIFIED|  
  
## <a name="applies-to"></a>套用至  
 [Open 方法 (ADO Connection)](./open-method-ado-connection.md)
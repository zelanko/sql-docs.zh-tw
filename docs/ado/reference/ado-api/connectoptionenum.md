---
title: ConnectOptionEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 819fb89d7f8c43e76ba9260a72fafa68084bf880
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67933442"
---
# <a name="connectoptionenum"></a>ConnectOptionEnum
指定[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件的[開啟](../../../ado/reference/ado-api/open-method-ado-connection.md)方法是否應在建立連接（同步）或之前（非同步）後傳回。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adAsyncConnect**|16|會以非同步方式開啟連接。 [ConnectComplete](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)事件可以用來判斷連接何時可用。|  
|**adConnectUnspecified**|-1|預設。 會以同步方式開啟連接。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等  
 Package： **.com. wfc. 資料**  
  
|持續性|  
|--------------|  
|AdoEnums.ConnectOption.ASYNCCONNECT|  
|AdoEnums.ConnectOption.CONNECTUNSPECIFIED|  
  
## <a name="applies-to"></a>套用至  
 [Open 方法 (ADO Connection)](../../../ado/reference/ado-api/open-method-ado-connection.md)

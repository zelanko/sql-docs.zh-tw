---
title: MultiIpConfigurationSupport 屬性 （ServerNetworkProtocol 類別） |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: wmi
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- MultiIpConfigurationSupport Property (ServerNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- MultiIpConfigurationSupport property
ms.assetid: 442c6133-4038-42db-a67d-2631285ac76b
caps.latest.revision: 31
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: d0ab21380ac5898a11bf41d24d40e7bf48f2a920
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33008645"
---
# <a name="multiipconfigurationsupport-property-servernetworkprotocol-class"></a>MultiIpConfigurationSupport 屬性 (ServerNetworkProtocol 類別)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  取得布林屬性，該屬性可指定伺服器網路通訊協定是否支援多個 IP 位址。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.MultiIpConfigurationSupport [= value]  
```  
  
## <a name="parts"></a>組件  
 *物件*  
 A [ProtocolName 屬性 （ServerNetworkProtocol 類別）](../../../relational-databases/wmi-provider-configuration-classes/servernetworkprotocol-class/protocolname-property-servernetworkprotocol-class.md)物件的執行個體所使用之網路通訊協定[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 布林值，指定伺服器網路通訊協定是否支援多個 IP 位址： **true**如果伺服器網路通訊協定支援多個 IP 位址或**false**如果伺服器網路通訊協定不支援多個 IP 位址。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定伺服器網路通訊協定和網路程式庫](http://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  

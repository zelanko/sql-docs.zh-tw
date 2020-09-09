---
description: MultiIpConfigurationSupport 屬性 (ServerNetworkProtocol 類別)
title: 'MultiIpConfigurationSupport 屬性 (ServerNetworkProtocol) '
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- MultiIpConfigurationSupport Property (ServerNetworkProtocol
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- MultiIpConfigurationSupport property
ms.assetid: 442c6133-4038-42db-a67d-2631285ac76b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9a0c29f72ab66f008dfe6ddfb87be054501aeb50
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545442"
---
# <a name="multiipconfigurationsupport-property-servernetworkprotocol-class"></a>MultiIpConfigurationSupport 屬性 (ServerNetworkProtocol 類別)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  取得布林屬性，該屬性可指定伺服器網路通訊協定是否支援多個 IP 位址。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.MultiIpConfigurationSupport [= value]  
```  
  
## <a name="parts"></a>組件  
 *object*  
 [ProtocolName 屬性 (ServerNetworkProtocol 類別) ](../../../relational-databases/wmi-provider-configuration-classes/servernetworkprotocol-class/protocolname-property-servernetworkprotocol-class.md)物件，代表實例所使用的網路通訊協定 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 布林值，指定伺服器網路通訊協定是否支援多個 IP 位址：如果伺服器網路通訊協定支援多個 IP 位址， **則為 true** ; 如果伺服器網路通訊協定不支援多個 ip 位址，則為 **false** 。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定伺服器網路通訊協定與網路程式庫](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  

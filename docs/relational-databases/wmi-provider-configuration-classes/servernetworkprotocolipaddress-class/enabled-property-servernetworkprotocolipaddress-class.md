---
description: Enabled 屬性 (ServerNetworkProtocolIpAddress 類別)
title: 'Enabled 屬性 (ServerNetworkProtocolIpAddress) '
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- Enabled Property (ServerNetworkProtocolIpAddress Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- Enabled property
ms.assetid: 870fd4d0-6c77-462a-b480-d42eb044b2e7
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 585601724ebc34139c554bde6c85d14028e5e05e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88485196"
---
# <a name="enabled-property-servernetworkprotocolipaddress-class"></a>Enabled 屬性 (ServerNetworkProtocolIpAddress 類別)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  取得布林屬性，該屬性會指定是否啟用 IP 位址。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.Enabled [= value]  
```  
  
## <a name="parts"></a>組件  
 *object*  
 代表實例上網路通訊協定之 IP 位址的 [ServerNetworkProtocolIPAdress 類別](../../../relational-databases/wmi-provider-configuration-classes/servernetworkprotocolipaddress-class/servernetworkprotocolipaddress-class.md) 物件 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 指定是否啟用 IP 位址的布林值：如果已啟用 IP 位址， **則為 true** ; 如果已停用 ip 位址，則為 **false** 。  
  
## <a name="see-also"></a>另請參閱  
 [設定伺服器網路通訊協定與網路程式庫](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  

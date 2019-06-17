---
title: 啟用屬性 （ServerNetworkProtocolIpAddress 類別） |Microsoft Docs
ms.custom: ''
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
manager: craigg
ms.openlocfilehash: 57a467de4cfe05232a73fd42a40b401c71c8c6fa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62751686"
---
# <a name="enabled-property-servernetworkprotocolipaddress-class"></a>Enabled 屬性 (ServerNetworkProtocolIpAddress 類別)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  取得布林屬性，該屬性會指定是否啟用 IP 位址。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.Enabled [= value]  
```  
  
## <a name="parts"></a>組件  
 *object*  
 A [ServerNetworkProtocolIPAdress 類別](../../../relational-databases/wmi-provider-configuration-classes/servernetworkprotocolipaddress-class/servernetworkprotocolipaddress-class.md)物件，表示執行個體上的網路通訊協定的 IP 位址[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 布林值，指定是否啟用 IP 位址：**真**如果已啟用的 IP 位址，或**false**如果已停用的 IP 位址。  
  
## <a name="see-also"></a>另請參閱  
 [設定伺服器網路通訊協定和網路程式庫](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  

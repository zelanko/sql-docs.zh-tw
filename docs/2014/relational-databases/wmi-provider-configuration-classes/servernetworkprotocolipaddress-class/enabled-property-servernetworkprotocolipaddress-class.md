---
title: 啟用屬性 （ServerNetworkProtocolIpAddress 類別） |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Enabled Property (ServerNetworkProtocolIpAddress Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- Enabled property
ms.assetid: 870fd4d0-6c77-462a-b480-d42eb044b2e7
caps.latest.revision: 14
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 655acfd106800927bbec8b2fa8021a3b2ba4be87
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36133378"
---
# <a name="enabled-property-servernetworkprotocolipaddress-class"></a>Enabled 屬性 (ServerNetworkProtocolIpAddress 類別)
  取得布林屬性，該屬性會指定是否啟用 IP 位址。  
  
## <a name="syntax"></a>語法  
  
```  
  
object  
.Enabled [= value]  
```  
  
## <a name="parts"></a>組件  
 *object*  
 A [ServerNetworkProtocolIPAdress 類別](servernetworkprotocolipaddress-class.md)物件，代表執行個體上網路通訊協定之 IP 位址[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 指定是否啟用 IP 位址的布林值：如果要啟用 IP 位址為 `true`，如果要停用 IP 位址則為 `false`。  
  
## <a name="see-also"></a>另請參閱  
 [設定伺服器網路通訊協定和網路程式庫](http://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
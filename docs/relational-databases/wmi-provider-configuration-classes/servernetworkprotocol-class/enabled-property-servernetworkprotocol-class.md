---
description: Enabled 屬性 (ServerNetworkProtocol 類別)
title: 'Enabled 屬性 (ServerNetworkProtocol) '
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- Enabled Property (ServerNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- Enabled property
ms.assetid: a514822a-91f1-4aca-9175-2b96cff29700
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0da8f0be827c4d65ee675be81116655cb42ef69e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88446232"
---
# <a name="enabled-property-servernetworkprotocol-class"></a>Enabled 屬性 (ServerNetworkProtocol 類別)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  取得布林屬性，該屬性會指定是否啟用伺服器網路通訊協定。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.Enabled [= value]  
```  
  
## <a name="parts"></a>組件  
 *object*  
 代表實例所使用之網路通訊協定的 [ServerNetworkProtocol 類別](../../../relational-databases/wmi-provider-configuration-classes/servernetworkprotocol-class/servernetworkprotocol-class.md) 物件 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 指定是否啟用伺服器網路通訊協定的布林值：如果已啟用伺服器網路通訊協定， **則為 true** ; 如果伺服器網路通訊協定已停用，則為 **false** 。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定伺服器網路通訊協定與網路程式庫](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  

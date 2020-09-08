---
description: SetDisable 方法 (ServerNetworkProtocolIPAddress 類別)
title: 'SetDisable 方法 (ServerNetworkProtocolIPAddress) '
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetDisable Method (ServerNetworkProtocolIPAddress Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetDisable method
ms.assetid: 7a7cc8cc-9fb8-4bf5-b483-2150d633ee10
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 2ce3332f08e8044ed6e4797eb144043de8f82e6c
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89516898"
---
# <a name="setdisable-method-servernetworkprotocolipaddress-class"></a>SetDisable 方法 (ServerNetworkProtocolIPAddress 類別)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  停用 IP 位址。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.SetDisable()  
```  
  
## <a name="parts"></a>組件  
 *object*  
 代表 [執行個體上網路通訊協定之 IP 位址的](../../../relational-databases/wmi-provider-configuration-classes/servernetworkprotocolipaddress-class/servernetworkprotocolipaddress-class.md) ServerNetworkProtocolIPAdress 類別 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]物件。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 uint32 值，如果已成功修改此服務為 0，如果不支援要求則為 1，以及其他指示錯誤的任何數字。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定伺服器網路通訊協定與網路程式庫](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  

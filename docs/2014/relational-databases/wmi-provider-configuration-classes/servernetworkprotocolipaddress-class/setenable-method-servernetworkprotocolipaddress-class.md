---
title: SetEnable 方法（ServerNetworkProtocolIPAddress 類別） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- SetEnable Method (ServerNetworkProtocolIPAddress Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetEnable method
ms.assetid: baa86deb-95dd-416f-b2c7-cec1dfb91ab4
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: d4c542aa1491710d49ec4c24c027e69f2eef24a9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62643117"
---
# <a name="setenable-method-servernetworkprotocolipaddress-class"></a>SetEnable 方法 (ServerNetworkProtocolIPAddress 類別)
  啟用 IP 位址。  
  
## <a name="syntax"></a>語法  
  
```  
  
object  
.SetEnable()  
  
```  
  
## <a name="parts"></a>組件  
 *目標*  
 代表實例上網路通訊協定之[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]IP 位址的[ServerNetworkProtocolIPAdress 類別](servernetworkprotocolipaddress-class.md)物件。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 
  `uint32` 值，如果已成功修改此服務為 0，如果不支援要求則為 1，以及其他指示錯誤的任何數字。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定伺服器網路通訊協定與網路程式庫](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  

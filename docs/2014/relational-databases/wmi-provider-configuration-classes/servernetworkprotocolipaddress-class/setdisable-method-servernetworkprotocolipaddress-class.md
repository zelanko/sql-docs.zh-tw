---
title: SetDisable 方法（ServerNetworkProtocolIPAddress 類別） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- SetDisable Method (ServerNetworkProtocolIPAddress Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetDisable method
ms.assetid: 7a7cc8cc-9fb8-4bf5-b483-2150d633ee10
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 9fbe928de1144c3065ddabb07bfd48606fdcea51
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85059752"
---
# <a name="setdisable-method-servernetworkprotocolipaddress-class"></a>SetDisable 方法 (ServerNetworkProtocolIPAddress 類別)
  停用 IP 位址。  
  
## <a name="syntax"></a>語法  
  
```  
  
object  
.SetDisable()  
  
```  
  
## <a name="parts"></a>組件  
 *object*  
 [ServerNetworkProtocolIPAdress 類別] servernetworkprotocolipaddress-class.md）物件，代表實例上網路通訊協定的 IP 位址 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 uint32 值，如果已成功修改此服務為 0，如果不支援要求則為 1，以及其他指示錯誤的任何數字。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定伺服器網路通訊協定與網路程式庫](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  

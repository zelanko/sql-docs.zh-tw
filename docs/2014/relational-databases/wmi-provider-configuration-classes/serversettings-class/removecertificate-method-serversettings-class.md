---
title: RemoveCertificate 方法（ServerSettings 類別） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- RemoveCertificate Method (ServerSettings Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- RemoveCertificate method
ms.assetid: 9ffdbc39-93f5-48fb-859a-86a3ad545827
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 9fb16415d3422035f67722f36c05cca10d1a3248
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62735901"
---
# <a name="removecertificate-method-serversettings-class"></a>RemoveCertificate 方法 (ServerSettings 類別)
  從 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]執行個體中移除目前的安全性憑證。  
  
## <a name="syntax"></a>語法  
  
```  
  
object  
.RemoveCertificate()  
  
```  
  
## <a name="parts"></a>組件  
 *目標*  
 表示 [執行個體上之伺服器設定的](serversettings-class.md) ServerSettings 類別 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]物件。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 u`int32` 值，如果已成功修改此服務為 0，如果不支援要求則為 1，以及其他指示錯誤的任何數字。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定伺服器網路通訊協定與網路程式庫](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
